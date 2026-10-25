---
type: interview
series: Java Interview
part: 5
tags: [java, interview]
---

# 🧵 Java Core Interview Reference — Part 5: Multithreading & Concurrency

> [!info] **Part 5 of 9** — Threads, synchronization, the Java Memory Model, executors
> Previous: [[01 - Java/Interview/04 - Exceptions & Generics|Part 4 — Exceptions & Generics]] | Hub: [[01 - Java/Interview/00 - Overview|Interview Hub]]
> Tags: #java #interview #core-java #concurrency

> [!danger] This is the hardest part of the series — and the one that decides senior interviews. Read it slowly.

---

## 📑 Table of Contents

- [[#🧵 Section 1 — Thread Basics (Q317–Q330)]]
- [[#🔒 Section 2 — Synchronization & Locks (Q331–Q346)]]
- [[#🧠 Section 3 — Java Memory Model & volatile (Q347–Q358)]]
- [[#💀 Section 4 — Deadlock, Livelock & Starvation (Q359–Q366)]]
- [[#⚙️ Section 5 — Executors & Thread Pools (Q367–Q380)]]
- [[#🧰 Section 6 — Concurrency Utilities (Q381–Q392)]]
- [[#🚀 Section 7 — CompletableFuture & Virtual Threads (Q393–Q400)]]
- [[#🧩 Section 8 — Quick Fire Round]]

---

# 🧵 Section 1 — Thread Basics (Q317–Q330)

## ❓ Q317. Process vs Thread? ⭐

| | Process | Thread |
|---|---------|--------|
| Memory | own address space | **shares** heap with other threads |
| Creation cost | heavy | light |
| Communication | IPC (slow) | shared memory (fast, but risky) |
| Crash impact | isolated | can corrupt the whole process |
| Owns | resources | a stack + program counter |

Each thread has its **own stack** and **own PC**, but shares the **heap**, **metaspace**, and **static fields**. That sharing is the source of every concurrency bug. ⚠️

---

## ❓ Q318. How do you create a thread? Which way is better? ⭐⭐

```java
// 1. extend Thread — ❌ uses up your single inheritance slot
class MyThread extends Thread { public void run() { } }
new MyThread().start();

// 2. implement Runnable — ✅ preferred
class MyTask implements Runnable { public void run() { } }
new Thread(new MyTask()).start();

// 3. lambda — ✅ cleanest
new Thread(() -> System.out.println("running")).start();

// 4. Callable + ExecutorService — ✅ best for real work (returns a value + exceptions)
ExecutorService pool = Executors.newFixedThreadPool(4);
Future<Integer> f = pool.submit(() -> 42);
```

**Why `Runnable` over `Thread`?** Separates the **task** from the **execution mechanism**, keeps inheritance free, and lets you reuse the task in a thread pool.

---

## ❓ Q319. `start()` vs `run()`? ⭐⭐ (classic trap)

- `start()` → asks the JVM to create a **new OS thread** and call `run()` there
- `run()` → just a normal method call **on the current thread**. No concurrency at all.

```java
t.run();     // runs on main thread — nothing parallel happens
t.start();   // ✅ truly concurrent
```

---

## ❓ Q320. What happens if you call `start()` twice?

`IllegalThreadStateException`. A thread's lifecycle is one-way — a dead thread can never be restarted.

---

## ❓ Q321. `Runnable` vs `Callable`? ⭐

| | `Runnable` | `Callable<V>` |
|---|-----------|---------------|
| Method | `void run()` | `V call() throws Exception` |
| Returns value | ❌ | ✅ |
| Throws checked exceptions | ❌ | ✅ |
| Since | 1.0 | 1.5 |
| Used with | `Thread`, `execute()` | `submit()`, returns a `Future` |

---

## ❓ Q322. What are the thread states? ⭐⭐

```
   NEW ──start()──► RUNNABLE ◄────────────────┐
                    │   ▲                     │
     wait/join/     │   │ notify / timeout /  │
     lock needed    ▼   │ lock acquired       │
              BLOCKED / WAITING / TIMED_WAITING
                    │
                run() ends
                    ▼
                TERMINATED
```

| State | Meaning |
|---|---|
| `NEW` | created, not started |
| `RUNNABLE` | running or ready to run (Java does not distinguish "ready" and "running") |
| `BLOCKED` | waiting for a **monitor lock** (`synchronized`) |
| `WAITING` | `wait()`, `join()`, `park()` with no timeout |
| `TIMED_WAITING` | `sleep(n)`, `wait(n)`, `join(n)` |
| `TERMINATED` | finished |

---

## ❓ Q323. `sleep()` vs `wait()`? ⭐⭐⭐ (asked everywhere)

| | `sleep()` | `wait()` |
|---|-----------|----------|
| Class | `Thread` (static) | `Object` |
| **Releases the lock?** | ❌ **NO** | ✅ **YES** |
| Needs synchronized block | ❌ | ✅ (else `IllegalMonitorStateException`) |
| Wakes up by | time expiry / interrupt | `notify()`, `notifyAll()`, timeout, interrupt |
| Purpose | pause | inter-thread communication |

> [!danger] The single sentence that gets you the point: **`sleep()` keeps the lock, `wait()` releases it.**

---

## ❓ Q324. `wait()`, `notify()`, `notifyAll()` — how are they used?

```java
synchronized (lock) {
    while (!condition) {      // ⭐ ALWAYS a while loop, never if
        lock.wait();
    }
    // proceed
}

synchronized (lock) {
    condition = true;
    lock.notifyAll();
}
```

**Why `while` not `if`?** Because of **spurious wakeups** (the JVM may wake a thread without notify) and because another thread may have consumed the condition before you re-acquired the lock. Re-checking is mandatory. 🔁

---

## ❓ Q325. `notify()` vs `notifyAll()`?

- `notify()` wakes **one arbitrary** waiting thread — risk of waking the "wrong" one and causing a hang
- `notifyAll()` wakes **all** — safer, slightly more overhead

**Default to `notifyAll()`** unless you can prove all waiters are interchangeable.

---

## ❓ Q326. Why are `wait/notify` defined on `Object`, not `Thread`?

Because the lock (**monitor**) belongs to an **object**, not to a thread. Every object in Java has a monitor, so wait/notify must live on `Object`.

---

## ❓ Q327. What does `join()` do?

Makes the current thread wait for another thread to finish.

```java
t1.start(); t2.start();
t1.join(); t2.join();      // main waits for both
System.out.println("both done");
```

---

## ❓ Q328. What is `yield()`?

A **hint** to the scheduler that this thread is willing to give up the CPU. Platform dependent and mostly useless in production. It does **not** release locks.

---

## ❓ Q329. What is a daemon thread? ⭐

A background thread that does **not** prevent the JVM from exiting.

```java
t.setDaemon(true);   // must be called BEFORE start()
t.start();
```
When only daemon threads remain, the JVM exits **immediately** — `finally` blocks may not run. Examples: the GC thread, timers, monitoring.

---

## ❓ Q330. What is thread priority?

`Thread.MIN_PRIORITY`(1) … `NORM_PRIORITY`(5) … `MAX_PRIORITY`(10). It is only a **hint** to the OS scheduler — behaviour differs per platform. Never build logic on priorities. ⚠️

---

# 🔒 Section 2 — Synchronization & Locks (Q331–Q346)

## ❓ Q331. What is a race condition? ⭐

Two threads access shared mutable data and at least one writes; the result depends on timing.

```java
count++;   // NOT atomic — it is read, add, write (3 steps)
```
Two threads can both read 5, both write 6 → one increment is **lost**.

---

## ❓ Q332. What is `synchronized` and how does it work? ⭐⭐

It acquires the **monitor** of an object. Only one thread can hold a given monitor at a time.

```java
synchronized void m() { }          // locks `this`
static synchronized void s() { }   // locks THE CLASS object (MyClass.class)
synchronized (lockObject) { }      // locks a specific object ✅ preferred
```

> [!warning] Instance and static synchronized methods use **different locks** — they do not block each other.

Under the hood: `monitorenter` / `monitorexit` bytecode instructions, backed by an object header **mark word** that can be biased, thin (CAS), or inflated to an OS mutex.

---

## ❓ Q333. What does `synchronized` guarantee besides mutual exclusion? ⭐

**Visibility** — entering a synchronized block gives you everything written before the previous thread exited it (happens-before). Mutual exclusion alone would not be enough without this memory guarantee. 🧠

---

## ❓ Q334. Why is `synchronized(this)` risky in library code?

Any external code holding a reference to your object can also lock on it and cause a deadlock you cannot see. Use a **private final lock object**:

```java
private final Object lock = new Object();
synchronized (lock) { ... }
```

---

## ❓ Q335. Can you synchronize a constructor?

No — a constructor is not accessible to multiple threads before the object exists. You may use a synchronized block **inside** it, but that usually signals a design problem.

---

## ❓ Q336. What is the double-checked locking singleton and why does it need `volatile`? ⭐⭐

```java
class Singleton {
    private static volatile Singleton instance;    // ⭐ volatile is MANDATORY
    static Singleton getInstance() {
        if (instance == null) {                    // 1st check — no lock, fast
            synchronized (Singleton.class) {
                if (instance == null)              // 2nd check — under lock
                    instance = new Singleton();
            }
        }
        return instance;
    }
}
```

**Why `volatile`?** `new Singleton()` is three steps: allocate memory, run the constructor, assign the reference. The JVM may **reorder** steps 2 and 3. Without `volatile`, another thread could see a **non-null but not-yet-constructed** object. 💥

> [!tip] Better singletons: an `enum` (Part 2, Q150) or the **holder idiom**:
> ```java
> private static class Holder { static final Singleton INSTANCE = new Singleton(); }
> static Singleton getInstance() { return Holder.INSTANCE; }
> ```
> Lazy, thread-safe, and lock-free — the JVM guarantees class initialization is atomic.

---

## ❓ Q337. `synchronized` vs `ReentrantLock`? ⭐⭐

| | `synchronized` | `ReentrantLock` |
|---|----------------|-----------------|
| Syntax | keyword, automatic release | explicit `lock()` / `unlock()` |
| Try without blocking | ❌ | ✅ `tryLock()` |
| Timeout | ❌ | ✅ `tryLock(1, SECONDS)` |
| Interruptible | ❌ | ✅ `lockInterruptibly()` |
| Fairness | ❌ | ✅ optional `new ReentrantLock(true)` |
| Multiple conditions | one wait set | ✅ many `Condition` objects |
| Release on exception | automatic | **you must use `finally`** ⚠️ |

```java
lock.lock();
try { /* work */ }
finally { lock.unlock(); }     // ⭐ ALWAYS in finally
```

---

## ❓ Q338. What does "reentrant" mean?

A thread that already holds a lock can acquire it again without deadlocking. Both `synchronized` and `ReentrantLock` are reentrant — essential for recursion and for calling one synchronized method from another.

---

## ❓ Q339. What is `ReadWriteLock`?

Many readers **or** one writer.

```java
ReadWriteLock rw = new ReentrantReadWriteLock();
rw.readLock().lock();    // shared
rw.writeLock().lock();   // exclusive
```
Great for read-heavy caches. `StampedLock` (Java 8) adds an even faster **optimistic read** mode.

---

## ❓ Q340. What is lock striping?

Splitting one lock into many so different keys can be updated in parallel — exactly what `ConcurrentHashMap` does per bucket.

---

## ❓ Q341. What is an atomic operation? What is CAS? ⭐

**CAS = Compare-And-Swap**, a single CPU instruction: "if the value is still X, set it to Y; otherwise fail and let me retry."

```java
AtomicInteger count = new AtomicInteger();
count.incrementAndGet();                  // lock-free, thread-safe ✅
count.compareAndSet(5, 10);
count.updateAndGet(x -> x * 2);
```

**Advantage:** no blocking, no context switch. **Disadvantage:** under very high contention, threads spin and burn CPU.

---

## ❓ Q342. What is the ABA problem?

A value changes A → B → A. CAS sees "still A" and succeeds, but the world changed in between (common with pointers/stacks). Fix: `AtomicStampedReference` adds a version counter. 🏷️

---

## ❓ Q343. What atomic classes exist?

`AtomicInteger`, `AtomicLong`, `AtomicBoolean`, `AtomicReference`, `AtomicIntegerArray`, `AtomicStampedReference`, and the Java 8 high-contention counters **`LongAdder`** / `DoubleAdder`.

> [!tip] `LongAdder` beats `AtomicLong` under heavy contention because it spreads updates across multiple cells and only sums them on `sum()`.

---

## ❓ Q344. Is `i++` atomic on a `volatile int`?

**No.** `volatile` gives visibility, **not atomicity**. `i++` is still read-modify-write. Use `AtomicInteger` or `synchronized`.

---

## ❓ Q345. What is thread confinement?

Avoiding sharing entirely — the safest concurrency strategy. `ThreadLocal` is the explicit tool:

```java
private static final ThreadLocal<SimpleDateFormat> FORMAT =
    ThreadLocal.withInitial(() -> new SimpleDateFormat("yyyy-MM-dd"));
```

> [!danger] `ThreadLocal` + thread pools = **memory leak**. Pooled threads live forever, so the value is never released. Always `remove()` in a `finally`.

---

## ❓ Q346. Which common classes are NOT thread-safe?

`SimpleDateFormat` (famous!), `ArrayList`, `HashMap`, `StringBuilder`, `Calendar`. Use `DateTimeFormatter` (immutable, Java 8) instead of `SimpleDateFormat`. ✅

---

# 🧠 Section 3 — Java Memory Model & volatile (Q347–Q358)

## ❓ Q347. What is the Java Memory Model (JMM)? ⭐⭐

The specification that defines **when** a write by one thread becomes **visible** to another, and which reorderings the compiler/CPU may perform.

Without it, each CPU core could keep values in its own cache forever and other threads would never see updates. 🧊

---

## ❓ Q348. What is the visibility problem?

```java
class Worker {
    private boolean running = true;      // ❌ not volatile
    void stop() { running = false; }
    void run() { while (running) { } }   // may loop FOREVER
}
```
The JIT may hoist `running` into a register and never re-read it. Adding `volatile` fixes it.

---

## ❓ Q349. What does `volatile` do? ⭐⭐

1. **Visibility** — every read goes to main memory, every write is flushed to it
2. **Ordering** — prevents reordering across the volatile access (memory barriers)
3. **Atomicity for 64-bit** — makes `long`/`double` reads and writes atomic

**What it does NOT do:** make compound operations (`i++`, check-then-act) atomic. 🚫

---

## ❓ Q350. `volatile` vs `synchronized`? ⭐

| | `volatile` | `synchronized` |
|---|-----------|----------------|
| Mutual exclusion | ❌ | ✅ |
| Visibility | ✅ | ✅ |
| Blocking | ❌ never | ✅ can block |
| Applies to | variables only | methods & blocks |
| Performance | cheap | more expensive |
| Use case | status flags, DCL | compound state updates |

---

## ❓ Q351. What is the happens-before relationship? ⭐⭐

If A *happens-before* B, then everything A wrote is visible to B. The main rules:

1. **Program order** — within one thread, statements happen in order
2. **Monitor lock** — unlocking happens-before a later locking of the same monitor
3. **volatile** — a write happens-before every later read of that field
4. **Thread start** — `t.start()` happens-before everything in `t`
5. **Thread join** — everything in `t` happens-before `t.join()` returns
6. **Transitivity** — if A→B and B→C then A→C
7. **Final fields** — properly constructed final fields are visible without synchronization

---

## ❓ Q352. What is instruction reordering?

The compiler, JIT, and CPU may reorder instructions for speed as long as the **single-threaded** result is unchanged. Other threads can observe the reordered order — the cause of many concurrency bugs. `volatile`, `synchronized`, and `final` insert barriers that limit it.

---

## ❓ Q353. What is safe publication?

Making an object visible to other threads such that they see it **fully constructed**. Safe ways:
- Initialize it in a `static` initializer
- Store it in a `volatile` or `final` field
- Store it in an `AtomicReference`
- Guard it with a lock
- Put it into a thread-safe collection

---

## ❓ Q354. Why does `final` help concurrency?

The JMM guarantees that correctly constructed `final` fields are visible to all threads **without synchronization** — as long as `this` did not escape during the constructor.

---

## ❓ Q355. What is "this escaping" in a constructor?

Publishing `this` before the constructor finishes (registering a listener, starting a thread inside the constructor) lets other threads see a half-built object. Use a static factory that constructs first and registers after. ⚠️

---

## ❓ Q356. Are `long` and `double` writes atomic?

**Not guaranteed** without `volatile` on 32-bit JVMs — a thread could see the high 32 bits of one value and the low 32 bits of another (**word tearing**). All other primitives and references are atomic.

---

## ❓ Q357. What is false sharing?

Two independent variables sit in the **same CPU cache line**; updating one invalidates the cache for the other core. It kills performance silently. `@Contended` (JDK internal) or padding fixes it. 🧱

---

## ❓ Q358. Is an immutable object automatically thread-safe?

**Yes**, provided it is properly constructed (all fields `final`, no `this` escape, defensive copies). This is why immutability is the strongest concurrency tool. 🛡️

---

# 💀 Section 4 — Deadlock, Livelock & Starvation (Q359–Q366)

## ❓ Q359. What is deadlock? ⭐⭐

Two or more threads each hold a lock the other needs, so nobody can proceed.

```java
// Thread 1                    // Thread 2
synchronized (A) {             synchronized (B) {
    synchronized (B) { }           synchronized (A) { }   // 💀 deadlock
}                              }
```

---

## ❓ Q360. What are the four Coffman conditions?

Deadlock requires **all four** at once:
1. **Mutual exclusion** — resources are exclusive
2. **Hold and wait** — hold one while waiting for another
3. **No preemption** — locks cannot be forcibly taken
4. **Circular wait** — a cycle of dependencies

Break **any one** and deadlock becomes impossible. 🔓

---

## ❓ Q361. How do you prevent deadlock? ⭐

1. ✅ **Lock ordering** — always acquire locks in a global, consistent order (breaks circular wait)
2. ✅ **`tryLock` with timeout** — back off and retry (breaks hold-and-wait)
3. ✅ Hold locks for the **shortest** time possible
4. ✅ Avoid **nested** locks entirely
5. ✅ Use higher-level constructs (`ConcurrentHashMap`, executors, immutable objects) instead of raw locks

---

## ❓ Q362. How do you detect a deadlock in production?

- `jstack <pid>` → it explicitly prints "Found one Java-level deadlock"
- JConsole / VisualVM → "Detect Deadlock" button
- `ThreadMXBean.findDeadlockedThreads()` programmatically
- A thread dump shows threads `BLOCKED` on monitors owned by each other

---

## ❓ Q363. Deadlock vs Livelock vs Starvation? ⭐

| | Deadlock | Livelock | Starvation |
|---|----------|----------|------------|
| Threads are | blocked, doing nothing | **busy**, but making no progress | waiting forever for CPU/lock |
| Analogy | two cars stuck at a junction | two people repeatedly stepping aside for each other | a low-priority thread never scheduled |
| Fix | lock ordering | randomized backoff | fair locks |

---

## ❓ Q364. What is a fair lock and what does it cost?

`new ReentrantLock(true)` serves threads in FIFO arrival order — no starvation, but **significantly slower** because it prevents barging and causes more context switches.

---

## ❓ Q365. What is thread interruption? ⭐

A cooperative **request** to stop — not a forced kill.

```java
t.interrupt();                          // sets the interrupt flag

// inside the thread:
while (!Thread.currentThread().isInterrupted()) { ... }

try { Thread.sleep(1000); }
catch (InterruptedException e) {
    Thread.currentThread().interrupt();   // ⭐ RESTORE the flag, do not swallow!
    return;
}
```

> [!warning] Catching `InterruptedException` **clears** the flag. If you swallow it, the shutdown signal is lost and your service will not stop cleanly.

---

## ❓ Q366. Why are `stop()`, `suspend()`, and `resume()` deprecated?

`stop()` kills a thread mid-operation, releasing all its locks and leaving shared data **corrupted**. `suspend()` keeps the locks while frozen → guaranteed deadlock. Use interruption + a `volatile` flag instead. ☠️

---

# ⚙️ Section 5 — Executors & Thread Pools (Q367–Q380)

## ❓ Q367. Why use a thread pool instead of `new Thread()`? ⭐

- Thread creation is expensive (~1 MB stack each + OS call)
- Unbounded thread creation → `OutOfMemoryError` under load
- Pools give **reuse**, **bounded concurrency**, **queueing**, and **lifecycle management**

---

## ❓ Q368. What are the built-in `Executors` factories?

| Factory | Behaviour |
|---|---|
| `newFixedThreadPool(n)` | n threads, **unbounded queue** ⚠️ |
| `newCachedThreadPool()` | grows without limit, 60s idle timeout ⚠️ |
| `newSingleThreadExecutor()` | 1 thread, sequential, unbounded queue |
| `newScheduledThreadPool(n)` | delayed and periodic tasks |
| `newWorkStealingPool()` | ForkJoinPool with parallelism = cores |
| `newVirtualThreadPerTaskExecutor()` | Java 21 — a virtual thread per task |

> [!danger] Why senior engineers avoid these factories
> `newFixedThreadPool` uses an **unbounded** `LinkedBlockingQueue` → under overload, tasks pile up until `OutOfMemoryError`. `newCachedThreadPool` creates **unlimited threads**. In production, build a `ThreadPoolExecutor` manually with a **bounded queue** and an explicit rejection policy.

---

## ❓ Q369. Explain the `ThreadPoolExecutor` parameters. ⭐⭐

```java
new ThreadPoolExecutor(
    corePoolSize,        // threads kept alive even when idle
    maximumPoolSize,     // upper limit
    keepAliveTime, unit, // idle timeout for threads above core
    workQueue,           // where tasks wait
    threadFactory,       // naming, daemon flag ⭐ name your threads!
    rejectionHandler);
```

**Task arrival logic (the order matters!):**
1. Threads < core → **create a new thread**
2. Else → **put in the queue**
3. Queue full → create threads up to **max**
4. Max reached and queue full → **reject**

> [!warning] Counter-intuitive: with an **unbounded** queue, `maximumPoolSize` is never reached — step 3 never happens.

---

## ❓ Q370. What are the rejection policies?

| Policy | Behaviour |
|---|---|
| `AbortPolicy` (default) | throws `RejectedExecutionException` |
| `CallerRunsPolicy` | the submitting thread runs it → natural backpressure ✅ |
| `DiscardPolicy` | silently drops it 🤫 |
| `DiscardOldestPolicy` | drops the oldest queued task |

---

## ❓ Q371. How do you size a thread pool? ⭐

- **CPU-bound:** `threads ≈ number of cores` (or cores + 1)
- **I/O-bound:** `cores × (1 + waitTime / computeTime)` — can be much larger
- `Runtime.getRuntime().availableProcessors()` gives the core count

Always measure; the formula is a starting point, not a law.

---

## ❓ Q372. `execute()` vs `submit()`? ⭐

| | `execute()` | `submit()` |
|---|-------------|------------|
| Accepts | `Runnable` | `Runnable` or `Callable` |
| Returns | `void` | `Future` |
| Exceptions | go to the uncaught handler / printed | **captured in the Future** — silent until `get()` ⚠️ |

---

## ❓ Q373. How do you shut down an executor properly? ⭐

```java
pool.shutdown();                                   // no new tasks; finish existing
if (!pool.awaitTermination(30, TimeUnit.SECONDS)) {
    pool.shutdownNow();                            // interrupt running tasks
}
```
`shutdown()` vs `shutdownNow()`: the first is graceful, the second interrupts and returns the queued tasks that never ran.

> [!warning] Non-daemon pool threads keep the JVM alive forever if you never shut down.

---

## ❓ Q374. What is a `Future`? What are its limits?

```java
Future<Integer> f = pool.submit(() -> compute());
Integer result = f.get(5, TimeUnit.SECONDS);   // BLOCKS
f.cancel(true);  f.isDone();  f.isCancelled();
```
**Limits:** `get()` blocks, no callbacks, no chaining, no combining. `CompletableFuture` solves all of these.

---

## ❓ Q375. What is `invokeAll()` / `invokeAny()`?

- `invokeAll(tasks)` → runs all, blocks until **all** complete, returns a list of Futures
- `invokeAny(tasks)` → returns the result of the **first** to succeed, cancels the rest

---

## ❓ Q376. What is `ScheduledExecutorService`?

```java
sched.schedule(task, 5, SECONDS);                        // once
sched.scheduleAtFixedRate(task, 0, 1, SECONDS);          // every 1s from START time
sched.scheduleWithFixedDelay(task, 0, 1, SECONDS);       // 1s AFTER previous finishes
```
`AtFixedRate` can bunch up tasks if one run is slow; `WithFixedDelay` never overlaps.

---

## ❓ Q377. What is the ForkJoinPool and work stealing? ⭐

Designed for **divide and conquer**. Each worker has its own deque; an idle worker **steals** tasks from the *tail* of a busy worker's deque, which minimizes contention.

```java
class SumTask extends RecursiveTask<Long> {
    protected Long compute() {
        if (small enough) return computeDirectly();
        SumTask left = new SumTask(...), right = new SumTask(...);
        left.fork();                      // async
        return right.compute() + left.join();
    }
}
```
`parallelStream()` uses the **common ForkJoinPool** by default. ⚠️ Never run blocking I/O in a parallel stream — you starve the shared pool for the whole JVM.

---

## ❓ Q378. `RecursiveTask` vs `RecursiveAction`?

`RecursiveTask<V>` returns a value; `RecursiveAction` returns nothing.

---

## ❓ Q379. How do you name threads in a pool and why does it matter?

```java
ThreadFactory tf = r -> { Thread t = new Thread(r, "order-worker-" + n++); return t; };
```
Because a production thread dump full of `pool-1-thread-7` tells you nothing. Naming threads is a small habit that marks an experienced engineer. 🏷️

---

## ❓ Q380. What happens if a task throws inside a pool thread?

- With `execute()` → the thread dies, the pool creates a replacement, and the uncaught handler fires
- With `submit()` → the exception is stored in the `Future` and is **invisible** until `get()`. This is why bugs silently vanish in pools. Always log inside the task or check the Future.

---

# 🧰 Section 6 — Concurrency Utilities (Q381–Q392)

## ❓ Q381. What is `CountDownLatch`? ⭐

A one-shot gate: wait until N events happen.

```java
CountDownLatch latch = new CountDownLatch(3);
// workers: latch.countDown();
latch.await();      // main waits for all 3
```
**Cannot be reset.** Use case: wait for all services to boot before accepting traffic.

---

## ❓ Q382. What is `CyclicBarrier`? How is it different from `CountDownLatch`? ⭐

| | `CountDownLatch` | `CyclicBarrier` |
|---|------------------|-----------------|
| Reusable | ❌ one-shot | ✅ resets automatically |
| Who waits | usually one waiter, many counters | **all parties wait for each other** |
| Barrier action | ❌ | ✅ runs a task when the barrier trips |

```java
CyclicBarrier barrier = new CyclicBarrier(3, () -> System.out.println("round done"));
barrier.await();   // each thread blocks until all 3 arrive
```

---

## ❓ Q383. What is `Semaphore`?

A permit counter that limits concurrent access.

```java
Semaphore sem = new Semaphore(5);      // 5 permits
sem.acquire();
try { useResource(); } finally { sem.release(); }
```
Use: connection pools, rate limiting, bounding parallelism.

---

## ❓ Q384. What is `Exchanger`?

Two threads swap objects at a rendezvous point. Rare, used in pipeline/buffer-swapping designs.

---

## ❓ Q385. What is `Phaser`?

A more flexible `CyclicBarrier` — the number of parties can change dynamically, and it supports multiple phases.

---

## ❓ Q386. How do you implement producer-consumer? ⭐⭐

```java
BlockingQueue<Task> queue = new ArrayBlockingQueue<>(100);

// Producer
queue.put(task);          // blocks if full

// Consumer
Task t = queue.take();    // blocks if empty
```
The blocking queue handles all the waiting and signalling — no `wait/notify` needed. This is the answer interviewers want. ✅

**Manual version (if they ask for wait/notify):**
```java
synchronized (lock) {
    while (queue.size() == CAPACITY) lock.wait();
    queue.add(item);
    lock.notifyAll();
}
```

---

## ❓ Q387. What `BlockingQueue` implementations exist?

| Class | Note |
|---|---|
| `ArrayBlockingQueue` | bounded, one lock |
| `LinkedBlockingQueue` | optionally bounded, separate put/take locks (better throughput) |
| `PriorityBlockingQueue` | unbounded, ordered |
| `SynchronousQueue` | zero capacity — a direct handoff |
| `DelayQueue` | elements become available after a delay |
| `LinkedTransferQueue` | most flexible/fastest |

---

## ❓ Q388. What concurrent collections exist?

`ConcurrentHashMap`, `ConcurrentSkipListMap` (sorted), `CopyOnWriteArrayList`, `CopyOnWriteArraySet`, `ConcurrentLinkedQueue`/`Deque` (non-blocking, CAS-based), `ConcurrentHashMap.newKeySet()`.

---

## ❓ Q389. What is `ThreadLocalRandom`?

A per-thread random generator. `Math.random()` and a shared `Random` have a single internal seed updated by CAS → contention. `ThreadLocalRandom.current().nextInt(10)` avoids it entirely. ⚡

---

## ❓ Q390. What is `AbstractQueuedSynchronizer` (AQS)?

The framework behind `ReentrantLock`, `Semaphore`, `CountDownLatch`, and `ReadWriteLock`. It maintains an `int state` plus a FIFO queue of waiting threads, using CAS on the state. Knowing this name signals depth. 🎓

---

## ❓ Q391. What is `LockSupport.park()/unpark()`?

Low-level thread blocking primitives used by AQS. Unlike `wait/notify`, `unpark` can be called **before** `park` and the permit is remembered — no lost-wakeup problem.

---

## ❓ Q392. What is `StampedLock`?

Java 8 lock with three modes: write, read, and **optimistic read** (no lock at all — you read, then `validate(stamp)` and retry if a write happened). Very fast for read-dominated data. Not reentrant. ⚠️

---

# 🚀 Section 7 — CompletableFuture & Virtual Threads (Q393–Q400)

## ❓ Q393. What is `CompletableFuture`? ⭐

A `Future` you can compose, chain, and combine — non-blocking async programming.

```java
CompletableFuture.supplyAsync(() -> fetchUser(id))
    .thenApply(User::getEmail)                       // transform
    .thenCompose(email -> sendAsync(email))          // chain another future (flatMap)
    .thenCombine(otherFuture, (a, b) -> a + b)       // combine two
    .exceptionally(ex -> "fallback")                 // handle errors
    .thenAccept(System.out::println);                // consume
```

---

## ❓ Q394. `thenApply` vs `thenCompose` vs `thenCombine`?

| Method | Analogy | Signature |
|---|---|---|
| `thenApply` | `map` | `T → U` |
| `thenCompose` | `flatMap` | `T → CompletableFuture<U>` (avoids nesting) |
| `thenCombine` | `zip` | combines two independent futures |

---

## ❓ Q395. What is the difference between the `Async` variants?

`thenApply` may run on the thread that completed the previous stage; `thenApplyAsync` always submits to the pool (ForkJoinPool.commonPool by default, or one you pass). Use the `Async` variant with your **own executor** for blocking work. ✅

---

## ❓ Q396. How do you wait for many futures?

```java
CompletableFuture.allOf(f1, f2, f3).join();    // all complete (returns Void)
CompletableFuture.anyOf(f1, f2).join();        // first one
```

---

## ❓ Q397. How do you handle exceptions in `CompletableFuture`?

```java
.exceptionally(ex -> defaultValue)             // recover
.handle((result, ex) -> ex != null ? fallback : result)   // both cases
.whenComplete((result, ex) -> log(...))        // side effect, does not change the result
```

---

## ❓ Q398. What are virtual threads? (Java 21) ⭐

Lightweight threads managed by the **JVM**, not the OS. You can run **millions** of them.

```java
Thread.startVirtualThread(() -> handle(request));
var executor = Executors.newVirtualThreadPerTaskExecutor();
```

**Key idea:** when a virtual thread blocks on I/O, the JVM **unmounts** it from its carrier (platform) thread instead of blocking the OS thread. So blocking code becomes cheap again — you write simple synchronous code and get async scalability. 🎉

---

## ❓ Q399. What changes with virtual threads?

- ❌ **Thread pools become unnecessary** for I/O tasks — create a thread per task
- ⚠️ **`synchronized` can "pin"** a virtual thread to its carrier (improved in later JDKs); prefer `ReentrantLock` in hot paths
- ⚠️ `ThreadLocal` is still supported but costly at millions of threads
- ✅ Ideal for I/O-bound servers; **no benefit** for CPU-bound work

---

## ❓ Q400. Platform thread vs virtual thread?

| | Platform | Virtual |
|---|---------|---------|
| Backed by | one OS thread | a JVM continuation on a carrier thread |
| Cost | ~1 MB stack | a few hundred bytes, growable heap stack |
| Practical count | thousands | **millions** |
| Best for | CPU-bound | I/O-bound |
| Pooling | needed | ❌ anti-pattern |

---

# 🧩 Section 8 — Quick Fire Round

> [!question]- Can two threads execute two different synchronized methods of the SAME object at the same time?
> No — both need the same object monitor.

> [!question]- Can a thread execute a synchronized method while another executes a non-synchronized one?
> Yes. Non-synchronized methods do not check the lock at all.

> [!question]- Does `sleep()` release the lock?
> No. Only `wait()` does.

> [!question]- What happens if you call `wait()` outside a synchronized block?
> `IllegalMonitorStateException`.

> [!question]- Is `Vector` enough to be thread-safe in real use?
> No — individual methods are safe, but `if (!v.contains(x)) v.add(x)` is still a race.

> [!question]- Is `ConcurrentHashMap`'s `size()` exact?
> It is an estimate under concurrent modification — weakly consistent by design.

> [!question]- What is a memory barrier / fence?
> A CPU instruction that prevents reordering across it; inserted by `volatile` and lock operations.

> [!question]- What is the difference between concurrency and parallelism?
> Concurrency = dealing with many things at once (structure). Parallelism = doing many things at once (execution).

> [!question]- What is an immutable object's biggest concurrency advantage?
> Zero synchronization needed — it can be shared freely.

> [!question]- Can `finally` fail to run in a killed thread?
> Yes — daemon threads at JVM exit, or `Thread.stop()`.

> [!question]- Should you use `Timer` for scheduled tasks?
> No — one thread, and one exception kills all future tasks. Use `ScheduledExecutorService`.

> [!question]- What is the "common pool" and why is it dangerous?
> The shared `ForkJoinPool.commonPool()` used by parallel streams — blocking in it starves the entire JVM.

---

## 🎓 Self-Test Checklist for Part 5

- [ ] I can explain `start()` vs `run()` and `sleep()` vs `wait()` instantly
- [ ] I know all 6 thread states and what moves between them
- [ ] I can write double-checked locking and explain why `volatile` is required
- [ ] I can list the happens-before rules
- [ ] I can explain the 4 Coffman conditions and 3 ways to prevent deadlock
- [ ] I can explain every `ThreadPoolExecutor` parameter and the task-arrival order
- [ ] I know why `Executors.newFixedThreadPool` is dangerous in production
- [ ] I can implement producer-consumer with `BlockingQueue` from memory
- [ ] I can explain virtual threads and when they help

---

> [!success] ✅ Part 5 complete — Q317–Q400
> 👉 Next: [[01 - Java/Interview/06 - JVM|Part 6 — JVM]]

#java #interview #core-java #concurrency #part5
