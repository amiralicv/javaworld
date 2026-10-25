---
type: interview
series: Java Interview
part: 9
tags: [java, interview]
---

# 🎯 Java Core Interview Reference — Part 9: Design Patterns & Output Puzzles

> [!info] **Part 9 of 9** — Design patterns, tricky output questions, coding round prep, and the final review sheet
> Previous: [[01 - Java/Interview/08 - IO & Reflection|Part 8 — IO & Reflection]] | Hub: [[01 - Java/Interview/00 - Overview|Interview Hub]]
> Tags: #java #interview #core-java #patterns #puzzles

---

## 📑 Table of Contents

- [[#🏗️ Section 1 — Creational Patterns (Q621–Q632)]]
- [[#🧱 Section 2 — Structural Patterns (Q633–Q642)]]
- [[#🎭 Section 3 — Behavioural Patterns (Q643–Q654)]]
- [[#🧠 Section 4 — Principles & Anti-Patterns (Q655–Q662)]]
- [[#🧨 Section 5 — Output Puzzles (Q663–Q690)]]
- [[#💻 Section 6 — Coding Round Classics]]
- [[#🗣️ Section 7 — Behavioural & Closing Questions]]
- [[#🏁 Section 8 — The Final Review Sheet]]

---

# 🏗️ Section 1 — Creational Patterns (Q621–Q632)

## ❓ Q621. What are design patterns and the three categories?

Reusable solutions to recurring design problems.

| Category | Purpose | Examples |
|---|---|---|
| **Creational** | how objects are created | Singleton, Factory, Builder, Prototype |
| **Structural** | how objects are composed | Adapter, Decorator, Facade, Proxy, Composite |
| **Behavioural** | how objects communicate | Strategy, Observer, Template, Command, Iterator |

---

## ❓ Q622. Singleton — show the correct implementations. ⭐⭐

```java
// 1. Enum — BEST ✅ (thread-safe, serialization-safe, reflection-safe)
public enum Config { INSTANCE; public void load() { } }

// 2. Holder idiom — best for lazy loading ✅
public class Singleton {
    private Singleton() { }
    private static class Holder { static final Singleton INSTANCE = new Singleton(); }
    public static Singleton getInstance() { return Holder.INSTANCE; }
}

// 3. Double-checked locking — needs volatile ⚠️
private static volatile Singleton instance;
```

**How can a singleton be broken?** Reflection (`setAccessible` on the private constructor), serialization (creates a new object — fix with `readResolve`), cloning (fix by throwing in `clone`), and multiple classloaders. The `enum` version resists all of these. 🛡️

---

## ❓ Q623. Where is Singleton used in the JDK?

`Runtime.getRuntime()`, `Desktop.getDesktop()`, `System.getSecurityManager()`, logger factories.

---

## ❓ Q624. Why do many people call Singleton an anti-pattern?

It introduces **global mutable state**, makes unit testing hard (you cannot inject a fake), hides dependencies, and often causes concurrency problems. In modern code, a **DI container** manages a single instance for you without the global access point. ⚠️

---

## ❓ Q625. Factory Method pattern? ⭐

A method that decides which concrete class to instantiate, so callers depend only on the interface.

```java
interface Notification { void send(String msg); }

class NotificationFactory {
    static Notification create(String type) {
        return switch (type) {
            case "EMAIL" -> new EmailNotification();
            case "SMS"   -> new SmsNotification();
            default -> throw new IllegalArgumentException(type);
        };
    }
}
```
**JDK examples:** `Calendar.getInstance()`, `NumberFormat.getInstance()`, `valueOf()` methods, `List.of()`.

---

## ❓ Q626. Abstract Factory vs Factory Method?

Factory Method creates **one** product; Abstract Factory creates a **family** of related products (e.g. a `WindowsUIFactory` producing matching buttons, checkboxes, and menus).

---

## ❓ Q627. Builder pattern? ⭐⭐

For objects with many optional parameters — replaces the "telescoping constructor" problem.

```java
public class Pizza {
    private final String size;  private final boolean cheese, bacon;
    private Pizza(Builder b) { this.size = b.size; this.cheese = b.cheese; this.bacon = b.bacon; }

    public static class Builder {
        private final String size;              // required
        private boolean cheese, bacon;          // optional
        public Builder(String size) { this.size = size; }
        public Builder cheese(boolean v) { this.cheese = v; return this; }   // ⭐ return this
        public Builder bacon(boolean v)  { this.bacon = v;  return this; }
        public Pizza build() {
            if (size == null) throw new IllegalStateException("size required");
            return new Pizza(this);
        }
    }
}
Pizza p = new Pizza.Builder("L").cheese(true).bacon(false).build();
```
**JDK examples:** `StringBuilder`, `Stream.Builder`, `HttpRequest.newBuilder()`, `Calendar.Builder`.

---

## ❓ Q628. When do you need a Builder?

Rule of thumb: **4+ constructor parameters**, or several optional ones, or you want immutability with readable construction. 🍕

---

## ❓ Q629. Prototype pattern?

Create new objects by **copying** an existing one instead of constructing from scratch (expensive initialization). Java's `clone()` is its native form — but a copy constructor is usually cleaner (Part 2, Q145).

---

## ❓ Q630. What is a static factory method and its advantages over constructors? ⭐

```java
Integer.valueOf(5);   List.of(1,2);   Optional.of(x);   Instant.now();
```
**Advantages (*Effective Java*, Item 1):**
1. They have **names** (`newSortedList` vs another anonymous constructor)
2. They can **cache/reuse** instances (Integer cache!)
3. They can return a **subtype** (`List.of` returns different hidden classes by size)
4. They can vary the returned class by input

---

## ❓ Q631. Object Pool pattern?

Reuse expensive objects instead of recreating them — connection pools (HikariCP), thread pools. Only worth it when creation cost is genuinely high; for ordinary objects modern GC makes pooling **slower**. ⚠️

---

## ❓ Q632. Dependency Injection — what and why?

Dependencies are **passed in** rather than created inside.

```java
// ❌ tightly coupled — impossible to test with a fake
class Service { private final Repo repo = new MySqlRepo(); }
// ✅ injected
class Service { private final Repo repo; Service(Repo repo) { this.repo = repo; } }
```
Benefits: testability, loose coupling, easy swapping of implementations. **Constructor injection** is preferred over field injection (it makes dependencies explicit and allows `final`).

---

# 🧱 Section 2 — Structural Patterns (Q633–Q642)

## ❓ Q633. Adapter pattern? ⭐

Makes an incompatible interface usable — the "power plug converter". 🔌

```java
class LegacyPrinter { void printDoc(String s) { } }
class PrinterAdapter implements ModernPrinter {
    private final LegacyPrinter legacy;
    public void print(Document d) { legacy.printDoc(d.toText()); }
}
```
**JDK:** `Arrays.asList()`, `InputStreamReader` (bytes→chars), `Collections.list(Enumeration)`.

---

## ❓ Q634. Decorator pattern? ⭐

Adds behaviour by **wrapping**, without subclass explosion.

```java
new BufferedReader(new InputStreamReader(new FileInputStream(f)));
```
**JDK:** all of `java.io`, `Collections.unmodifiableList()`, `Collections.synchronizedList()`.

---

## ❓ Q635. Adapter vs Decorator vs Proxy — how do they differ?

| Pattern | Changes the interface? | Adds behaviour? | Intent |
|---|---|---|---|
| **Adapter** | ✅ yes | ❌ | make incompatible things work together |
| **Decorator** | ❌ same interface | ✅ yes | add responsibilities dynamically |
| **Proxy** | ❌ same interface | ✅ control | control access (lazy, remote, security) |

---

## ❓ Q636. Proxy pattern? ⭐

A stand-in that controls access to the real object.

Types: **virtual** (lazy loading — Hibernate lazy entities), **protection** (security checks), **remote** (RMI), **smart** (logging, caching, transactions — Spring AOP).

---

## ❓ Q637. Facade pattern?

One simple interface hiding a complicated subsystem. Example: a `OrderFacade.placeOrder()` that internally calls inventory, payment, shipping, and notification services.

---

## ❓ Q638. Composite pattern?

Treat individual objects and groups uniformly through a shared interface — file system trees, UI component hierarchies, menu structures. 🌳

---

## ❓ Q639. Flyweight pattern?

Share common state between many objects to save memory. **JDK:** `Integer.valueOf()` cache, the String pool, `Character.valueOf()`.

---

## ❓ Q640. Bridge pattern?

Separate an abstraction from its implementation so both can vary independently — e.g. `Shape` (abstraction) × `Renderer` (implementation) instead of `SquareVectorShape`, `SquareRasterShape`, ...

**JDK:** JDBC — `Driver` is the bridge between the API and each database.

---

## ❓ Q641. What is the difference between inheritance and the Decorator for adding features?

Inheritance is static and multiplies classes (`BufferedEncryptedFileReader`); decorators compose at runtime in any order. 🎁

---

## ❓ Q642. What patterns appear in Spring?

Singleton (bean scope), Factory (`BeanFactory`), Proxy (AOP/transactions), Template Method (`JdbcTemplate`, `RestTemplate`), Observer (`ApplicationEvent`), Strategy (pluggable implementations), Builder (`RestClient.builder()`).

---

# 🎭 Section 3 — Behavioural Patterns (Q643–Q654)

## ❓ Q643. Strategy pattern? ⭐⭐

Encapsulate interchangeable algorithms and select one at runtime.

```java
interface PaymentStrategy { void pay(BigDecimal amount); }
class Cart {
    private PaymentStrategy strategy;
    void checkout(BigDecimal amt) { strategy.pay(amt); }
}
cart.setStrategy(new CreditCardPayment());
```
In modern Java, a **lambda is a strategy**: `Comparator`, `Predicate`, and `Runnable` are all strategy objects. ✨

---

## ❓ Q644. Observer pattern? ⭐

One-to-many notification: when the subject changes, all observers are told.

```java
interface Observer { void update(Event e); }
class Subject {
    private final List<Observer> observers = new CopyOnWriteArrayList<>();  // ⭐ thread-safe
    void notifyAll(Event e) { observers.forEach(o -> o.update(e)); }
}
```
**JDK:** listeners in Swing, `PropertyChangeListener`, Spring events, reactive streams. (`java.util.Observer` is **deprecated** — do not use it.)

---

## ❓ Q645. Template Method pattern? ⭐

The parent defines the skeleton; subclasses fill in steps.

```java
abstract class DataProcessor {
    public final void process() {     // ⭐ final — the algorithm is fixed
        read(); transform(); write();
    }
    protected abstract void read();
    protected void transform() { }    // optional hook
    protected abstract void write();
}
```
**JDK:** `AbstractList`, `InputStream.read()`, `JdbcTemplate`, servlet `service()`.

---

## ❓ Q646. Strategy vs Template Method?

Strategy uses **composition** (swap the whole algorithm at runtime); Template Method uses **inheritance** (fix the skeleton, vary the steps at compile time).

---

## ❓ Q647. Command pattern?

Wrap a request as an object → enables queuing, logging, undo/redo. `Runnable` submitted to an `ExecutorService` is exactly this. Also used in transaction logs and GUI actions.

---

## ❓ Q648. Chain of Responsibility?

Pass a request along a chain until someone handles it — servlet filters, Spring Security filter chain, exception handlers, logging levels. ⛓️

---

## ❓ Q649. Iterator pattern?

Traverse a collection without exposing its internals — `java.util.Iterator` is the pattern built into the language.

---

## ❓ Q650. State pattern?

An object changes behaviour when its internal state changes, replacing large `if/switch` chains with state classes. Example: an order that is Draft → Paid → Shipped → Delivered, each with different allowed actions.

---

## ❓ Q651. Mediator pattern?

Centralizes communication so components do not reference each other directly — reduces N×N coupling to N.

---

## ❓ Q652. Memento pattern?

Capture and restore an object's state without exposing its internals — undo functionality, snapshots.

---

## ❓ Q653. Visitor pattern?

Add new operations to an object hierarchy without changing the classes. In Java 21, **sealed interfaces + switch pattern matching** largely replace it with far less code. 🆕

---

## ❓ Q654. Which patterns does the JDK use most? (a great answer to have ready)

| Pattern | JDK example |
|---|---|
| Singleton | `Runtime.getRuntime()` |
| Factory | `Calendar.getInstance()`, `List.of()` |
| Builder | `StringBuilder`, `HttpRequest.newBuilder()` |
| Adapter | `Arrays.asList()`, `InputStreamReader` |
| Decorator | `java.io` streams, `Collections.unmodifiableX` |
| Proxy | `java.lang.reflect.Proxy`, RMI |
| Strategy | `Comparator`, `Predicate` |
| Observer | listeners, Spring events |
| Template Method | `AbstractList`, `JdbcTemplate` |
| Iterator | `Iterator`, `Iterable` |
| Flyweight | `Integer.valueOf()` cache, String pool |

---

# 🧠 Section 4 — Principles & Anti-Patterns (Q655–Q662)

## ❓ Q655. What is DRY, KISS, YAGNI?

- **DRY** — Don't Repeat Yourself (one source of truth for each piece of knowledge)
- **KISS** — Keep It Simple, Stupid
- **YAGNI** — You Aren't Gonna Need It (do not build for imagined future requirements)

---

## ❓ Q656. What is the Law of Demeter?

"Talk only to your immediate friends." Avoid `a.getB().getC().getD().doThing()` — it couples you to the whole chain. Also called the **train wreck** anti-pattern. 🚂

---

## ❓ Q657. What are common anti-patterns? ⭐

- **God object** — one class doing everything
- **Spaghetti code** — no structure
- **Magic numbers** — unexplained literals
- **Premature optimization** — complexity with no measurement
- **Anemic domain model** — data classes with all logic in "services"
- **Copy-paste programming**
- **Exception swallowing** — `catch (Exception e) { }` 🚨

---

## ❓ Q658. What makes code testable?

Dependency injection, small functions with single responsibility, no hidden global state, no `new` inside business logic, deterministic behaviour (inject a `Clock` instead of calling `LocalDate.now()`). 🧪

---

## ❓ Q659. What is the difference between cohesion and coupling? (again — but say it well)

High cohesion inside a class, low coupling between classes. It is the single most reliable measure of a good design.

---

## ❓ Q660. What is composition over inheritance in one sentence?

Inheritance couples you to a parent's implementation forever; composition lets you swap behaviour and keeps encapsulation intact. (Part 2, Q75)

---

## ❓ Q661. What is "program to an interface, not an implementation"?

```java
List<String> list = new ArrayList<>();     // ✅ swap the implementation freely
ArrayList<String> list = new ArrayList<>(); // ❌ locks callers to ArrayList
```

---

## ❓ Q662. When is it acceptable to break a "best practice"?

When you have measured a real problem, understand the trade-off, and document why. Saying this shows engineering judgment rather than rule-following. 🎯

---

# 🧨 Section 5 — Output Puzzles (Q663–Q690)

> [!tip] Cover the answer, guess first, then open. This is the fastest way to find your blind spots.

> [!question]- **Q663.** `System.out.println(0.1 + 0.2 == 0.3);`
> **false** — IEEE 754 binary floating point.

> [!question]- **Q664.** `System.out.println('a' + 'b');`
> **195** — chars are promoted to int (97 + 98).

> [!question]- **Q665.** `System.out.println("" + 'a' + 'b');`
> **ab** — string concatenation, not addition.

> [!question]- **Q666.** `System.out.println(1 + 2 + "3" + 4 + 5);`
> **3345** — evaluated left to right.

> [!question]- **Q667.** `Integer a = 127, b = 127; Integer c = 128, d = 128; print(a==b, c==d);`
> **true false** — the Integer cache is −128 to 127.

> [!question]- **Q668.** `int i = 0; i = i++; print(i);`
> **0** — post-increment returns the old value, which overwrites the incremented one.

> [!question]- **Q669.** `System.out.println(Math.min(Double.MIN_VALUE, 0.0d));`
> **0.0** — `Double.MIN_VALUE` is the smallest **positive** value, not the most negative.

> [!question]- **Q670.** `System.out.println(Math.abs(Integer.MIN_VALUE));`
> **−2147483648** — the positive value does not fit in an int.

> [!question]- **Q671.** ```java int m() { try { return 1; } finally { return 2; } }```
> **2** — `finally`'s return wins.

> [!question]- **Q672.** ```java int m() { int x=1; try { return x; } finally { x=2; } }```
> **1** — the return value was already captured.

> [!question]- **Q673.** `String a = "ja"+"va"; String b = "java"; print(a==b);`
> **true** — compile-time constant folding puts it in the pool.

> [!question]- **Q674.** `String p="ja"; String a=p+"va"; print(a=="java");`
> **false** — runtime concatenation creates a new object. (Make `p` final → true.)

> [!question]- **Q675.** `System.out.println(new String("a") == "a");`
> **false** — `new` always creates a heap object outside the pool.

> [!question]- **Q676.** `List<Integer> l = new ArrayList<>(List.of(10,20,30)); l.remove(1); print(l);`
> **[10, 30]** — `remove(int)` removes by **index**.

> [!question]- **Q677.** `Set<Point> s; s.add(p); p.setX(9); print(s.contains(p));`
> **false** — the hash changed, so it looks in the wrong bucket.

> [!question]- **Q678.** `Parent p = new Child(); print(p.name);` where both declare `name`
> **Parent's name** — fields are resolved by the **reference type**.

> [!question]- **Q679.** `Parent p = new Child(); p.staticMethod();`
> **Parent's** — static methods are hidden, not overridden.

> [!question]- **Q680.** `System.out.println(Stream.of(1,2,3).allMatch(x -> x > 10));` on an **empty** stream
> On an empty stream `allMatch` returns **true** (vacuous truth).

> [!question]- **Q681.** ```java list.stream().filter(x -> {print(x); return true;});```
> **Nothing prints** — no terminal operation, so nothing executes.

> [!question]- **Q682.** `Optional.ofNullable(null).orElse(expensive());`
> `expensive()` **always runs**, even when the Optional has a value. Use `orElseGet`.

> [!question]- **Q683.** `System.out.println(0.0/0.0 == 0.0/0.0);`
> **false** — NaN is never equal to anything, including itself.

> [!question]- **Q684.** `byte a=10, b=20; byte c=a+b;`
> **Compile error** — `a+b` is promoted to int. `byte c = 10+20;` would compile (constant expression).

> [!question]- **Q685.** `System.out.println(-8 >> 1); System.out.println(-8 >>> 1);`
> **−4** and **2147483644**.

> [!question]- **Q686.** ```java for (String s : list) if (s.equals(secondLast)) list.remove(s);```
> **No exception**, but an element is silently skipped — the `hasNext()` quirk (Part 3, Q231).

> [!question]- **Q687.** `new HashSet<>(List.of("b","a","c"))` printed
> Order is **unspecified** — do not assume insertion or sorted order.

> [!question]- **Q688.** ```java class A { static { print("A"); } } class B extends A { static { print("B"); } } new B();```
> **A** then **B** — parent statics initialize first.

> [!question]- **Q689.** `System.out.println("1" + 2 + 3); System.out.println(1 + 2 + "3");`
> **123** and **33**.

> [!question]- **Q690.** ```java Integer x = null; int y = false ? 1 : x;```
> **NullPointerException** — the ternary unboxes `x`.

---

# 💻 Section 6 — Coding Round Classics

> [!note] These come up as live coding tasks. Practice writing them without an IDE.

**String / array**
1. Reverse a string (and in-place with a char array)
2. Check palindrome (ignore case and non-letters)
3. Count character frequency → `Map<Character,Integer>` with `merge`
4. Find the first non-repeating character → `LinkedHashMap`
5. Check if two strings are anagrams
6. Reverse the words in a sentence
7. Find duplicates in an array → `Set.add()` returns false
8. Find the missing number in 1..n → sum formula or XOR
9. Two Sum → `HashMap` of complement, O(n)
10. Move all zeros to the end

**Collections / logic**
11. Sort a `Map` by value
12. Group a list of objects by a field → `groupingBy`
13. Find the top K elements → min-heap of size K
14. Remove duplicates preserving order → `LinkedHashSet`
15. Implement an LRU cache → `LinkedHashMap` (Part 3, Q198)
16. Merge two sorted lists
17. Find the second largest element in one pass

**Classic algorithms**
18. Fibonacci — recursion, memoization, and iterative
19. Factorial (watch for overflow → use `BigInteger`)
20. Prime check + Sieve of Eratosthenes
21. Binary search (and the `left + (right-left)/2` overflow fix)
22. FizzBuzz (yes, still asked)
23. Detect a cycle in a linked list → fast/slow pointers
24. Balanced parentheses → `Deque` as a stack
25. Matrix rotation / spiral traversal

**Concurrency**
26. Producer-consumer with `BlockingQueue`
27. Print odd/even numbers with two alternating threads (`wait`/`notify`)
28. Thread-safe counter three ways: `synchronized`, `AtomicInteger`, `LongAdder`
29. Run N tasks and wait for all → `CountDownLatch` or `invokeAll`

**Design**
30. Design a thread-safe singleton
31. Design an immutable class
32. Implement `equals`/`hashCode` correctly
33. Design a parking lot / elevator / URL shortener (open-ended design)

---

# 🗣️ Section 7 — Behavioural & Closing Questions

> [!tip] These decide more offers than trivia does. Prepare one concrete story for each.

1. **"Tell me about a difficult bug you fixed."** → Structure: symptom → how you narrowed it → root cause → fix → what you changed so it cannot recur.
2. **"Describe a performance problem you solved."** → Mention measurement (profiler, GC logs) before the fix. Never say "I guessed."
3. **"A time you disagreed with a technical decision."** → Show you argued with data and then committed to the team's choice.
4. **"Code you are proud of / code you would rewrite."** → The second half shows growth.
5. **"How do you keep up with Java?"** → Name a specific source and a recent feature you tried.

**Questions to ask THEM** (asking nothing looks disengaged 🚩):
- What does the code review process look like?
- What is the biggest technical debt in the codebase right now?
- How do you handle production incidents?
- What does success look like for this role in 6 months?
- Which Java version are you on, and what stops you from upgrading?

---

# 🏁 Section 8 — The Final Review Sheet

> [!success] The 20 things you must be able to answer instantly

| # | Question | Part |
|---|---|---|
| 1 | JDK vs JRE vs JVM | 1 |
| 2 | Is Java pass-by-value? | 1 |
| 3 | Why is String immutable? | 1 |
| 4 | Integer cache −128..127 | 1 |
| 5 | Overloading vs overriding | 2 |
| 6 | equals/hashCode contract | 2 |
| 7 | Abstract class vs interface | 2 |
| 8 | How to make an immutable class | 2 |
| 9 | **HashMap internals** ⭐ | 3 |
| 10 | ArrayList vs LinkedList | 3 |
| 11 | fail-fast vs fail-safe / CME | 3 |
| 12 | Checked vs unchecked exceptions | 4 |
| 13 | try-with-resources + suppressed | 4 |
| 14 | Type erasure and PECS | 4 |
| 15 | sleep vs wait | 5 |
| 16 | volatile vs synchronized | 5 |
| 17 | ThreadPoolExecutor parameters | 5 |
| 18 | Heap generations + GC roots | 6 |
| 19 | map vs flatMap, lazy streams | 7 |
| 20 | Optional anti-patterns | 7 |

**The 48-hours-before checklist:**
- [ ] Re-read only the ⭐⭐ questions in each part
- [ ] Redo all 28 output puzzles in Section 5
- [ ] Write HashMap `put()` on paper from memory
- [ ] Write `equals`/`hashCode` on paper from memory
- [ ] Prepare 3 stories: a hard bug, a performance fix, a design decision
- [ ] Prepare 4 questions to ask them
- [ ] Sleep. A rested brain beats one more chapter. 😴

---

> [!success] 🎉 Series complete — Q1 through Q690 across 9 parts
> Go back to the hub: [[01 - Java/Interview/00 - Overview|Interview Hub]]
>
> **Final advice:** you will not be asked most of these. You will be asked five, and then asked to go three levels deeper on two of them. Depth beats coverage — pick your five strongest areas and make them unbreakable.

#java #interview #core-java #patterns #part9
