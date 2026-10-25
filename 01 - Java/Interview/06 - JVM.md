---
type: interview
series: Java Interview
part: 6
tags: [java, interview]
---

# 🧠 Java Core Interview Reference — Part 6: JVM, Memory & Garbage Collection

> [!info] **Part 6 of 9** — JVM architecture, memory areas, GC, class loading, performance
> Previous: [[01 - Java/Interview/05 - Concurrency|Part 5 — Concurrency]] | Hub: [[01 - Java/Interview/00 - Overview|Interview Hub]]
> Tags: #java #interview #core-java #jvm #gc

---

## 📑 Table of Contents

- [[#🏗️ Section 1 — JVM Architecture (Q401–Q410)]]
- [[#💾 Section 2 — Memory Areas (Q411–Q426)]]
- [[#🗑️ Section 3 — Garbage Collection (Q427–Q444)]]
- [[#📚 Section 4 — Class Loading (Q445–Q456)]]
- [[#🔧 Section 5 — Tuning & Troubleshooting (Q457–Q468)]]
- [[#🧩 Section 6 — Quick Fire Round]]

---

# 🏗️ Section 1 — JVM Architecture (Q401–Q410)

## ❓ Q401. Draw the JVM architecture. ⭐⭐

```
┌──────────────────────── JVM ─────────────────────────────┐
│                                                          │
│  1. CLASS LOADER SUBSYSTEM                               │
│     Loading → Linking (Verify, Prepare, Resolve) → Init  │
│                          │                               │
│  2. RUNTIME DATA AREAS   ▼                               │
│  ┌────────────────────┬──────────────────────────────┐   │
│  │ SHARED (all threads)│  PER-THREAD                 │   │
│  │  • Heap            │   • JVM Stack                │   │
│  │  • Metaspace       │   • PC Register              │   │
│  │  (Method Area)     │   • Native Method Stack      │   │
│  └────────────────────┴──────────────────────────────┘   │
│                          │                               │
│  3. EXECUTION ENGINE     ▼                               │
│     Interpreter │ JIT Compiler │ Garbage Collector       │
│                          │                               │
│  4. JNI  ←→  Native Method Libraries                     │
└──────────────────────────────────────────────────────────┘
```

---

## ❓ Q402. Which memory areas are shared and which are per-thread? ⭐

| Area | Shared? | Contents |
|---|---|---|
| **Heap** | ✅ shared | all objects, arrays, instance fields |
| **Metaspace** (Method Area) | ✅ shared | class metadata, static fields, constant pool |
| **JVM Stack** | ❌ per thread | frames: local variables, operand stack |
| **PC Register** | ❌ per thread | address of the current instruction |
| **Native Method Stack** | ❌ per thread | native (C/C++) call frames |

> [!tip] One-line memory rule: **objects on the heap, references on the stack.**

---

## ❓ Q403. What is inside a stack frame?

One frame per method call, containing:
1. **Local variable array** (including `this` for instance methods)
2. **Operand stack** (where bytecode does its arithmetic)
3. **Frame data** (constant pool reference, return address, exception table)

The frame is destroyed when the method returns — which is why locals need no GC. 🗑️

---

## ❓ Q404. Stack vs Heap? ⭐⭐

| | **Stack** | **Heap** |
|---|-----------|----------|
| Stores | primitives (locals), references, frames | objects, arrays, instance fields |
| Scope | per thread ✅ thread-safe | shared across threads ⚠️ |
| Allocation | LIFO, automatic | dynamic, managed by GC |
| Speed | very fast (pointer bump) | slower |
| Size | small (~512 KB–1 MB, `-Xss`) | large (`-Xmx`) |
| Error | `StackOverflowError` | `OutOfMemoryError` |
| Lifetime | until method returns | until unreachable + GC |

---

## ❓ Q405. Where are static variables stored?

The **metadata** lives in Metaspace, but since Java 8 the actual static field **values** are stored in the `java.lang.Class` object — which lives on the **heap**. [Certain] So static objects are collectible when their classloader is.

---

## ❓ Q406. Where do String literals live?

The **String Constant Pool**, which since Java 7 is part of the **heap** (before that, PermGen). This move was made specifically so that pooled strings can be garbage collected.

---

## ❓ Q407. What is the Execution Engine?

Three parts:
1. **Interpreter** — executes bytecode line by line; fast startup, slow repeated execution
2. **JIT compiler** — compiles hot methods to native code (C1 = fast compile, C2 = deep optimization; **tiered compilation** uses both)
3. **Garbage Collector** — reclaims unreachable objects

---

## ❓ Q408. What optimizations does the JIT perform?

- **Method inlining** (the most valuable one)
- **Escape analysis** → **scalar replacement** (an object that never escapes may never be allocated at all!)
- Dead code elimination, constant folding, loop unrolling
- Lock elision / biased locking
- Devirtualization of monomorphic calls

---

## ❓ Q409. What is `-XX:+PrintCompilation` / JITWatch used for?

Observing which methods get compiled, inlined, or deoptimized. Mentioning **deoptimization** (when the JIT's assumption is invalidated and it falls back to the interpreter) shows real depth. 🎓

---

## ❓ Q410. What is AOT and GraalVM native image?

Ahead-Of-Time compilation produces a native binary with near-instant startup and low memory — at the cost of losing runtime reflection flexibility (needs configuration) and peak JIT throughput. Popular for serverless and CLI tools.

---

# 💾 Section 2 — Memory Areas (Q411–Q426)

## ❓ Q411. What is the structure of the heap? ⭐⭐

```
┌──────────────── HEAP ─────────────────────────────┐
│  YOUNG GENERATION          │   OLD GENERATION     │
│ ┌────────┬──────┬───────┐  │ ┌──────────────────┐ │
│ │  Eden  │  S0  │  S1   │  │ │      Tenured     │ │
│ └────────┴──────┴───────┘  │ └──────────────────┘ │
│    ↑ new objects           │   ↑ long-lived       │
└────────────────────────────┴──────────────────────┘
                METASPACE (off-heap, native memory)
```
Default ratios: Young:Old ≈ 1:2, Eden:S0:S1 = 8:1:1.

---

## ❓ Q412. What is the generational hypothesis? ⭐

**"Most objects die young."** Empirically, the vast majority of objects become garbage almost immediately. So the JVM collects the young generation frequently and cheaply, and touches the old generation rarely. This single observation drives the entire GC design. 📉

---

## ❓ Q413. Walk me through an object's life in the heap. ⭐⭐

1. Allocated in **Eden** (via a fast pointer bump in a thread-local allocation buffer, **TLAB**)
2. Eden fills → **Minor GC**: live objects are copied to **Survivor S0**, everything else is freed
3. Next Minor GC: live objects from Eden **and** S0 move to **S1**; the age counter increments
4. Survivors ping-pong between S0 and S1, aging each time
5. Age reaches the **tenuring threshold** (default 15) → **promoted to Old Gen**
6. Old Gen fills → **Major/Full GC** (slower, longer pause)

**Also promoted early if:** the object is too big for Eden (**humongous**), or the survivor space overflows.

---

## ❓ Q414. Minor GC vs Major GC vs Full GC? ⭐

| | Minor (Young) GC | Major (Old) GC | Full GC |
|---|---|---|---|
| Collects | Young gen | Old gen | Young + Old + Metaspace |
| Frequency | often | rare | rarest |
| Pause | short (ms) | long | longest ⚠️ |
| Trigger | Eden full | Old gen threshold | promotion failure, `System.gc()`, metaspace full |

---

## ❓ Q415. What is a "stop-the-world" pause?

All application threads are paused so the GC can work on a consistent object graph. Every GC has some STW; modern collectors just make it shorter and more predictable. Threads stop at **safepoints** — well-defined bytecode positions where the thread state is known.

---

## ❓ Q416. What is a TLAB?

**Thread-Local Allocation Buffer** — each thread gets a private chunk of Eden so allocation needs no synchronization: just bump a pointer. That is why Java object allocation is often **faster than C's `malloc`**. ⚡

---

## ❓ Q417. What is Metaspace and how does it differ from PermGen? ⭐

| | PermGen (≤ Java 7) | Metaspace (Java 8+) |
|---|---|---|
| Location | inside the heap | **native memory** (off-heap) |
| Size | fixed (`-XX:MaxPermSize`) | grows automatically by default |
| Common error | `OutOfMemoryError: PermGen space` | `OutOfMemoryError: Metaspace` |
| String pool | inside it (≤ Java 6) | moved to the heap in Java 7 |

The change removed the most common tuning headache but did **not** remove classloader leaks — Metaspace can still grow until the machine dies. Bound it with `-XX:MaxMetaspaceSize`.

---

## ❓ Q418. What is the runtime constant pool?

Per-class table of literals and symbolic references (class names, method names, field names) built from the `.class` file's constant pool. It lives in Metaspace.

---

## ❓ Q419. What causes `StackOverflowError`?

Deep or infinite recursion; each call adds a frame. Increase with `-Xss2m`, but the real fix is usually converting recursion to iteration or making it tail-friendly (note: **Java has no tail-call optimization**).

---

## ❓ Q420. What are the different `OutOfMemoryError` messages? ⭐

| Message | Cause |
|---|---|
| `Java heap space` | genuine leak or heap too small |
| `GC overhead limit exceeded` | >98% time in GC, <2% memory recovered |
| `Metaspace` | too many classes (classloader leak) |
| `Direct buffer memory` | leaked `ByteBuffer.allocateDirect` |
| `unable to create new native thread` | OS thread/memory limit |
| `Requested array size exceeds VM limit` | array larger than ~`Integer.MAX_VALUE` |

---

## ❓ Q421. Can you have a memory leak in Java? ⭐⭐

**Yes** — GC only frees *unreachable* objects. A leak is an object you no longer need but still **reference**.

**Classic sources:**
1. **Static collections** that only ever grow (a cache with no eviction) 📈
2. **Unclosed resources** (streams, connections)
3. **Listeners/callbacks** never unregistered
4. **`ThreadLocal`** in a thread pool without `remove()`
5. **Inner class** holding an outer reference (Part 2, Q134)
6. Mutated keys in a `HashSet`/`HashMap` (Part 2, Q123)
7. **ClassLoader leaks** in app servers on redeploy
8. `substring()` in Java 6 (shared the parent char array — fixed in Java 7)

---

## ❓ Q422. What is `-Xms` and `-Xmx`?

Initial and maximum heap size. Setting them **equal** in production avoids resize pauses and makes behaviour predictable: `-Xms4g -Xmx4g`.

---

## ❓ Q423. What is off-heap memory?

Memory outside GC control: `ByteBuffer.allocateDirect()`, memory-mapped files, `Unsafe`. Used for zero-copy I/O and huge caches (Netty, Chronicle). It avoids GC pressure but you manage the lifetime yourself. ⚠️

---

## ❓ Q424. What is the object memory layout / how big is an object?

Roughly: **12-byte header** (mark word + class pointer with compressed oops) + fields + padding to a multiple of 8 bytes. An empty object is 16 bytes; an `Integer` is 16 bytes to hold a 4-byte value — which is why primitive collections libraries exist. 📦

---

## ❓ Q425. What are compressed oops?

On 64-bit JVMs with a heap under ~32 GB, references are stored as 32-bit offsets instead of 64-bit pointers — saving significant memory. This is why going from a 31 GB heap to a 33 GB heap can **reduce** effective capacity. 🤯

---

## ❓ Q426. Where do arrays live?

Always on the heap, even `int[]`. The reference to the array lives on the stack (if it's a local).

---

# 🗑️ Section 3 — Garbage Collection (Q427–Q444)

## ❓ Q427. What is garbage collection and when does an object become eligible? ⭐

An object is eligible when it is **unreachable from any GC root**.

**Common ways objects become eligible:**
```java
obj = null;                       // nulling the reference
obj = new Other();                // reassigning
void m() { Foo f = new Foo(); }   // going out of scope
// island of isolation: two objects referencing each other, nothing else references them ✅
```

---

## ❓ Q428. What are GC roots? ⭐⭐

The starting points for reachability analysis:
- Local variables and parameters in **active stack frames**
- **Static** fields of loaded classes
- **Active threads**
- JNI references (native code)
- Monitor objects held by synchronized blocks

---

## ❓ Q429. Reference counting vs reachability analysis? Why does Java use the latter?

Reference counting cannot free **circular references** (A→B→A) — a well-known leak source in Python and old COM. Java uses **reachability from roots**, so cycles are collected correctly as long as nothing outside points into them. ✅

---

## ❓ Q430. What are the reference types in Java? ⭐

| Type | Collected when | Use case |
|---|---|---|
| **Strong** `new Object()` | never while reachable | normal code |
| **Soft** `SoftReference` | only when memory is low | memory-sensitive caches |
| **Weak** `WeakReference` | at the next GC | `WeakHashMap`, metadata |
| **Phantom** `PhantomReference` | after finalization | replacement for `finalize()` cleanup |

```java
WeakReference<Data> ref = new WeakReference<>(data);
Data d = ref.get();      // may be null!
```

---

## ❓ Q431. Can you force garbage collection? ⭐

**No.** `System.gc()` is only a **suggestion** — the JVM may ignore it. Calling it in production is an anti-pattern: it often triggers an expensive Full GC. (`-XX:+DisableExplicitGC` disables it entirely.)

---

## ❓ Q432. What is `finalize()` and why is it dead?

A method the GC called before reclaiming an object. **Deprecated in Java 9, removed in Java 18.** Problems: no guarantee it ever runs, unpredictable timing, it can **resurrect** the object, it delays collection by a full extra GC cycle, and exceptions in it are swallowed. ☠️

**Use instead:** try-with-resources / `AutoCloseable`, or `java.lang.ref.Cleaner`.

---

## ❓ Q433. What GC algorithms exist? ⭐⭐

| Collector | Flag | Best for | Pause |
|---|---|---|---|
| **Serial** | `-XX:+UseSerialGC` | tiny heaps, single core, containers | long |
| **Parallel** (Throughput) | `-XX:+UseParallelGC` | batch jobs, max throughput | medium |
| **CMS** ☠️ removed in 14 | `-XX:+UseConcMarkSweepGC` | legacy low-pause | short |
| **G1** (default since Java 9) | `-XX:+UseG1GC` | general purpose, big heaps | predictable target |
| **ZGC** | `-XX:+UseZGC` | huge heaps (TB), ultra low pause | **<1 ms** |
| **Shenandoah** | `-XX:+UseShenandoahGC` | low pause, any heap size | <10 ms |
| **Epsilon** | `-XX:+UseEpsilonGC` | no-op, for benchmarking | n/a |

---

## ❓ Q434. What are the basic GC algorithms?

1. **Mark-Sweep** — mark reachable, free the rest → causes **fragmentation**
2. **Mark-Sweep-Compact** — plus moving survivors together → no fragmentation, slower
3. **Copying** — copy live objects to a new space → fast, wastes half the space (used in the young gen, where few survive)
4. **Generational** — different algorithms per age region

---

## ❓ Q435. How does G1 work? ⭐

G1 splits the heap into ~2048 equal **regions**, each dynamically labelled Eden, Survivor, Old, or Humongous.

- It marks concurrently, then collects the regions with the **most garbage first** ("Garbage First") 🥇
- It aims to meet a **pause target**: `-XX:MaxGCPauseMillis=200`
- It compacts incrementally, so no full-heap fragmentation
- Objects larger than half a region are "humongous" and allocated directly in Old

---

## ❓ Q436. How do ZGC and Shenandoah achieve sub-millisecond pauses?

They do marking **and relocation concurrently** with the application, using **load barriers** (ZGC) or **Brooks pointers** (Shenandoah) so threads always find the moved object. Pause time becomes independent of heap size — a 16 TB heap pauses as briefly as a 1 GB one. 🚀

---

## ❓ Q437. What is a write barrier / card table?

To avoid scanning the whole Old Gen during a Minor GC, the JVM tracks old→young references using a **card table** updated by a small **write barrier** on every reference store. Then only "dirty" cards are scanned. 🃏

---

## ❓ Q438. Does GC cause memory to return to the OS?

Historically no. Modern collectors (G1 with `-XX:+ShrinkHeapInSteps`, ZGC, Shenandoah) can **uncommit** unused memory — important in containers where you pay for RAM.

---

## ❓ Q439. What is the tenuring threshold?

The number of survived GC cycles before promotion (`-XX:MaxTenuringThreshold`, default 15). The JVM also adapts it dynamically based on survivor space occupancy.

---

## ❓ Q440. What is premature promotion and why is it bad?

When survivor space is too small, objects are promoted to Old Gen before they die → Old Gen fills quickly → frequent expensive Major GCs. Fix: enlarge the young gen or survivor ratio.

---

## ❓ Q441. What is a GC pause and how do you measure it?

Enable logging: `-Xlog:gc*:file=gc.log` (Java 9+) or `-XX:+PrintGCDetails` (Java 8). Analyze with GCViewer, GCEasy, or JFR. Look at **pause duration**, **frequency**, and **live set after Full GC** (that is your real memory need).

---

## ❓ Q442. Which GC should you choose? ⭐

- Small container / CLI → **Serial**
- Batch processing, throughput matters more than latency → **Parallel**
- Typical web service → **G1** (the default; usually correct)
- Latency-critical, large heap → **ZGC** or **Shenandoah**

> [!tip] The honest senior answer: "Start with the default G1 and a pause target. Do not change collectors until GC logs prove there is a problem."

---

## ❓ Q443. Is GC a stop-the-world for all collectors?

All have **some** STW phases (at minimum, root scanning). "Concurrent" collectors mean most work overlaps with the application, not that pauses are zero.

---

## ❓ Q444. What is escape analysis and stack allocation?

If the JIT proves an object never escapes its method, it can perform **scalar replacement** — breaking the object into plain local variables so it is never allocated on the heap at all, and never needs GC. This is why "avoid creating objects" advice is often outdated. 🎩

---

# 📚 Section 4 — Class Loading (Q445–Q456)

## ❓ Q445. What are the class loading phases? ⭐⭐

```
LOADING → LINKING (Verification → Preparation → Resolution) → INITIALIZATION
```

1. **Loading** — find the `.class` bytes, create the `Class` object
2. **Verification** — check the bytecode is valid and safe (this is a core Java security feature)
3. **Preparation** — allocate static fields and set them to **default** values (0/null) — *not* your assigned value yet
4. **Resolution** — replace symbolic references with direct ones (may be lazy)
5. **Initialization** — run static initializers and static field assignments, **in code order**

---

## ❓ Q446. What are the built-in class loaders? ⭐

| Loader | Loads from |
|---|---|
| **Bootstrap** | core JDK classes (`java.lang.*`); written in native code, `getClassLoader()` returns `null` |
| **Platform** (was Extension) | JDK platform modules |
| **Application/System** | your classpath |
| **Custom** | anything you want (app servers, plugins, hot reload) |

---

## ❓ Q447. What is the parent delegation model? ⭐⭐

A classloader **first asks its parent** to load the class, and only loads it itself if the parent cannot.

```
Application → Platform → Bootstrap
              (asks upward first, loads downward as fallback)
```

**Why?**
1. 🔒 **Security** — you cannot replace `java.lang.String` with your own version
2. ♻️ **Uniqueness** — a class is loaded once, avoiding duplicates

---

## ❓ Q448. What defines the identity of a class at runtime? ⭐

**Fully qualified name + the ClassLoader that loaded it.** The same `.class` file loaded by two different loaders produces two **incompatible** types — casting between them throws `ClassCastException` even though the code looks identical. This is the root of most app-server class loading mysteries. 😵

---

## ❓ Q449. When is a class initialized (static block run)? ⭐

Triggered by:
- `new` instance creation
- Accessing a **static method** or a **non-constant** static field
- Reflection (`Class.forName`)
- Initializing a subclass (initializes the parent first)
- Being the `main` class

**NOT triggered by:**
```java
Parent.staticFieldOfParent;      // accessing via a subclass initializes only the parent
Child[] arr = new Child[10];     // creating an array does NOT initialize the class
System.out.println(Foo.CONSTANT); // a `static final` COMPILE-TIME constant is inlined — no loading!
```

---

## ❓ Q450. `Class.forName()` vs `ClassLoader.loadClass()`?

- `Class.forName(name)` → loads **and initializes** (runs static blocks) ✅ — that is why old JDBC drivers were registered this way
- `loadClass(name)` → loads but does **not** initialize
- `Class.forName(name, false, loader)` → load without init

---

## ❓ Q451. Why write a custom ClassLoader?

Hot reloading, plugin isolation, loading classes from a database/network, encrypted class files, application servers isolating each deployed app.

```java
class MyLoader extends ClassLoader {
    protected Class<?> findClass(String name) {
        byte[] b = loadBytes(name);
        return defineClass(name, b, 0, b.length);
    }
}
```

---

## ❓ Q452. What is a ClassLoader leak?

When an app is redeployed, the old classloader must be collected. If **any** object from it is still referenced (a thread, a `ThreadLocal`, a static registry, a JDBC driver in the shared classloader), the entire classloader plus all its classes stays in Metaspace forever → `OutOfMemoryError: Metaspace` after a few redeploys. 🩸

---

## ❓ Q453. What breaks parent delegation and why?

**SPI (Service Provider Interface)** — `java.sql.DriverManager` is loaded by Bootstrap but must load driver implementations from the classpath, which Bootstrap cannot see. The fix is the **Thread Context ClassLoader**, which deliberately reverses the delegation. OSGi and app servers also break it for isolation.

---

## ❓ Q454. What is the JPMS module system? (Java 9)

`module-info.java` declares `requires` and `exports`, giving **strong encapsulation** (internal packages become truly inaccessible, not just discouraged) and reliable configuration at startup instead of classpath chaos.

```java
module com.myapp {
    requires java.sql;
    exports com.myapp.api;
}
```

---

## ❓ Q455. What is `static final` constant inlining?

```java
class Config { static final int MAX = 100; }   // compile-time constant
// Another class using Config.MAX gets the literal 100 baked into its bytecode.
```
Consequence: if you change `MAX` and recompile only `Config`, the other class still uses the **old value** until it is recompiled too. A real production trap. ⚠️

---

## ❓ Q456. What is bytecode verification protecting against?

Malicious or corrupt bytecode: stack overflows/underflows, illegal casts, accessing private members, jumping to invalid instructions. It is one of the pillars of the Java sandbox.

---

# 🔧 Section 5 — Tuning & Troubleshooting (Q457–Q468)

## ❓ Q457. What JVM tools do you know? ⭐

| Tool | Purpose |
|---|---|
| `jps` | list running JVMs |
| `jstat -gcutil <pid> 1s` | live GC statistics |
| `jstack <pid>` | thread dump (deadlocks, stuck threads) |
| `jmap -histo <pid>` | object histogram |
| `jmap -dump:live,file=heap.hprof <pid>` | heap dump |
| `jcmd <pid> ...` | the modern all-in-one tool ✅ |
| **JFR** (Java Flight Recorder) | low-overhead production profiling |
| **VisualVM / JMC / Eclipse MAT** | GUI analysis of dumps |
| `async-profiler` | flame graphs, very low overhead |

---

## ❓ Q458. How do you diagnose a memory leak? ⭐⭐

1. Confirm it: GC logs show the **live set after Full GC growing over time** 📈
2. Take two heap dumps hours apart: `jmap -dump:live,file=h1.hprof <pid>`
3. Open in **Eclipse MAT** → "Leak Suspects" report
4. Compare histograms — which class keeps growing?
5. Use **"Path to GC Roots"** (exclude weak/soft) on a sample instance to see *who is still holding it*
6. Fix the retaining reference

> [!tip] Say the phrase "**path to GC roots**" — it instantly shows you have done this for real.

---

## ❓ Q459. How do you diagnose high CPU usage?

1. `top -H -p <pid>` → find the hottest **thread ID**
2. Convert to hex: `printf '%x\n' <tid>`
3. `jstack <pid>` → find the matching `nid=0x...` and read its stack
4. Or just use `async-profiler` for a flame graph

Common causes: an infinite loop, GC thrashing, or a hash collision hot spot.

---

## ❓ Q460. What are the most useful JVM flags?

```bash
-Xms4g -Xmx4g                          # fixed heap
-XX:+UseG1GC -XX:MaxGCPauseMillis=200
-XX:MaxMetaspaceSize=512m
-XX:+HeapDumpOnOutOfMemoryError        # ⭐ ALWAYS enable in production
-XX:HeapDumpPath=/var/log/heap.hprof
-Xlog:gc*:file=gc.log:time,uptime:filecount=5,filesize=10m
-XX:+ExitOnOutOfMemoryError            # let the orchestrator restart it
```

---

## ❓ Q461. Why does the JVM ignore container memory limits (and how was it fixed)?

Old JVMs read the **host** CPU/memory, not the cgroup limit → they sized the heap for 64 GB inside a 512 MB container and got OOM-killed. Java 10+ is **container aware** by default (`-XX:+UseContainerSupport`).

Use ratios instead of absolutes in containers:
```bash
-XX:MaxRAMPercentage=75.0
```

---

## ❓ Q462. What is JMX?

Java Management Extensions — exposes MBeans for runtime monitoring and management (memory, threads, GC, custom metrics). Used by JConsole, Prometheus exporters, and APM tools.

---

## ❓ Q463. How do you reduce GC pressure in code?

- Avoid allocating in hot loops (reuse buffers)
- Pre-size collections
- Prefer primitives and primitive arrays over boxed collections
- Use `StringBuilder` in loops
- Stream carefully — boxing in `Stream<Integer>` vs `IntStream` matters
- Do not fear short-lived objects; the young gen handles them cheaply

---

## ❓ Q464. What is a heap dump vs a thread dump?

- **Heap dump** = snapshot of all objects and their references → for **memory** problems
- **Thread dump** = snapshot of all thread stacks and lock states → for **hangs, deadlocks, CPU** problems

---

## ❓ Q465. What does "live set" mean and why does it matter?

The bytes still reachable **after** a Full GC. It is your application's true memory requirement — the number you size `-Xmx` around (typically live set × 2–3).

---

## ❓ Q466. What are safepoints and safepoint pauses?

Points where all threads can be paused with a known state. Some operations (biased lock revocation, deoptimization, huge counted loops without a safepoint poll) cause **time-to-safepoint** delays that look like GC pauses but are not. `-Xlog:safepoint` reveals them. 🕵️

---

## ❓ Q467. What is JFR and why prefer it in production?

Java Flight Recorder collects detailed events (allocation, GC, locks, I/O, exceptions) at roughly **1% overhead**, so it can run continuously in production.

```bash
java -XX:StartFlightRecording=duration=60s,filename=rec.jfr MyApp
```

---

## ❓ Q468. What happens when the JVM starts, in order?

1. Parse the command line and create the JVM
2. Load core classes with the Bootstrap loader
3. Initialize the heap, GC, and JIT
4. Load the main class via the Application loader
5. Verify + prepare + initialize (run static blocks)
6. Invoke `main(String[])`
7. On exit: run shutdown hooks, then terminate (daemon threads are killed abruptly)

---

# 🧩 Section 6 — Quick Fire Round

> [!question]- Is memory allocated for a class or for an object?
> Class metadata → Metaspace at load time. Instance fields → heap at `new`.

> [!question]- Can the GC be forced?
> No. `System.gc()` is only a hint.

> [!question]- Does setting a reference to null guarantee immediate collection?
> No — it only makes the object *eligible*. Timing is the GC's choice.

> [!question]- Where is the String pool since Java 7?
> On the heap, so it can be garbage collected.

> [!question]- What is an "island of isolation"?
> A group of objects referencing each other but unreachable from any GC root — correctly collected by Java.

> [!question]- Which is the default GC in modern Java?
> G1 (since Java 9).

> [!question]- What replaced PermGen?
> Metaspace, in native memory, since Java 8.

> [!question]- Do local primitives get garbage collected?
> No — they live in the stack frame and disappear when the method returns.

> [!question]- What is the difference between `-Xmx` and `-XX:MaxRAMPercentage`?
> Absolute size vs a percentage of available RAM — the latter is container friendly.

> [!question]- Can Metaspace cause OOM?
> Yes — usually a classloader leak, or too many dynamically generated classes/proxies.

> [!question]- Does the JVM ever return memory to the OS?
> Modern collectors can uncommit unused heap; older ones generally do not.

> [!question]- What is deoptimization?
> The JIT discarding compiled code when an assumption (like a monomorphic call site) is invalidated, falling back to the interpreter.

---

## 🎓 Self-Test Checklist for Part 6

- [ ] I can draw the JVM architecture and the heap generations
- [ ] I can trace an object from Eden to Old Gen with the ages
- [ ] I can name 6 causes of memory leaks in Java
- [ ] I can explain GC roots and why reference cycles are not a problem
- [ ] I can compare Serial / Parallel / G1 / ZGC and choose one with reasons
- [ ] I can explain the 5 class loading phases and parent delegation
- [ ] I know that class identity = name + classloader
- [ ] I can describe a real memory-leak investigation using heap dumps and MAT
- [ ] I know the 5 JVM flags I would always set in production

---

> [!success] ✅ Part 6 complete — Q401–Q468
> 👉 Next: [[01 - Java/Interview/07 - Java 8 & Modern Java|Part 7 — Java 8 & Modern Java]]

#java #interview #core-java #jvm #gc #part6
