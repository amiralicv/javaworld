---
type: interview
series: Java Interview
part: 7
tags: [java, interview]
---

# 🚀 Java Core Interview Reference — Part 7: Java 8+ Modern Java

> [!info] **Part 7 of 9** — Lambdas, functional interfaces, Streams, Optional, Date/Time, and what came after Java 8
> Previous: [[01 - Java/Interview/06 - JVM|Part 6 — JVM]] | Hub: [[01 - Java/Interview/00 - Overview|Interview Hub]]
> Tags: #java #interview #core-java #java8 #streams

---

## 📑 Table of Contents

- [[#λ Section 1 — Lambdas (Q469–Q480)]]
- [[#🎛️ Section 2 — Functional Interfaces (Q481–Q492)]]
- [[#🌊 Section 3 — Streams (Q493–Q516)]]
- [[#📥 Section 4 — Collectors (Q517–Q526)]]
- [[#🎁 Section 5 — Optional (Q527–Q536)]]
- [[#📅 Section 6 — Date/Time API (Q537–Q544)]]
- [[#🆕 Section 7 — Java 9 to 21 Features (Q545–Q556)]]
- [[#🧩 Section 8 — Quick Fire Round]]

---

# λ Section 1 — Lambdas (Q469–Q480)

## ❓ Q469. What is a lambda expression? ⭐

An anonymous function — a block of behaviour you can pass around like data.

```java
// Before
Runnable r = new Runnable() { public void run() { System.out.println("hi"); } };
// After
Runnable r = () -> System.out.println("hi");
```

**Syntax forms:**
```java
() -> expression
x -> x * 2                     // one parameter, parentheses optional
(x, y) -> x + y
(String s) -> s.length()       // explicit type
(x, y) -> { return x + y; }    // block body needs return
```

---

## ❓ Q470. What problems do lambdas solve?

- Removes anonymous class boilerplate
- Enables **behaviour parameterization** (pass logic, not just data)
- Makes the Streams API possible
- Encourages a declarative style — say *what*, not *how*

---

## ❓ Q471. What can a lambda capture? ⭐

Local variables that are **final or effectively final**, plus instance/static fields (no restriction on those).

```java
int factor = 2;                       // effectively final ✅
list.forEach(x -> print(x * factor));
// factor = 3;                        // ❌ adding this breaks the lambda
```

**Why?** The value is copied into the lambda; allowing reassignment would create two inconsistent copies. Fields are fine because they are accessed through a reference. See Part 2, Q137.

---

## ❓ Q472. What does `this` mean inside a lambda? ⭐

The **enclosing instance** — unlike an anonymous class, where `this` is the anonymous object. Lambdas do not introduce a new scope; they are lexically scoped.

---

## ❓ Q473. How are lambdas compiled? Are they anonymous classes? ⭐

**No.** The compiler emits an `invokedynamic` instruction plus a private synthetic method. At first execution, `LambdaMetafactory` builds the implementation. Benefits: no extra `.class` file per lambda, and stateless lambdas can be **cached and reused** instead of allocated each time. 🎩

---

## ❓ Q474. What is a method reference? ⭐

Shorthand for a lambda that just calls one method.

| Kind | Syntax | Equivalent lambda |
|---|---|---|
| Static | `Integer::parseInt` | `s -> Integer.parseInt(s)` |
| Instance of a **particular** object | `System.out::println` | `x -> System.out.println(x)` |
| Instance of an **arbitrary** object | `String::toUpperCase` | `s -> s.toUpperCase()` |
| Constructor | `ArrayList::new` | `() -> new ArrayList<>()` |

---

## ❓ Q475. What is the difference between `String::length` and `str::length`?

`String::length` is unbound — the receiver becomes the first argument (`Function<String,Integer>`). `str::length` is bound to that specific object (`Supplier<Integer>`).

---

## ❓ Q476. Can a lambda throw a checked exception?

Only if the functional interface declares it. `Function`, `Consumer`, etc. do not — so you must handle it inside or wrap it (see Part 4, Q276).

---

## ❓ Q477. Can a lambda be recursive?

Not directly (it cannot reference itself during its own initialization). Workaround: assign to a field, or use a named method reference.

---

## ❓ Q478. Are lambdas slower than anonymous classes?

No. After JIT warmup they are typically **equal or faster**, partly due to caching of stateless lambdas and better inlining. Capturing lambdas allocate; non-capturing ones usually do not. ⚡

---

## ❓ Q479. What is behaviour parameterization? Give an example.

```java
// Instead of many filter methods:
static List<Apple> filter(List<Apple> apples, Predicate<Apple> p) {
    List<Apple> out = new ArrayList<>();
    for (Apple a : apples) if (p.test(a)) out.add(a);
    return out;
}
filter(apples, a -> a.getWeight() > 150);
filter(apples, a -> "red".equals(a.getColor()));
```

---

## ❓ Q480. When should you NOT use a lambda?

When the logic is long (extract a method), when you need state, when you need `this` to mean the function itself, or when a named method makes the intent clearer. A lambda longer than 3 lines is usually a mistake. ⚠️

---

# 🎛️ Section 2 — Functional Interfaces (Q481–Q492)

## ❓ Q481. What are the built-in functional interfaces? ⭐⭐

| Interface | Method | Meaning |
|---|---|---|
| `Predicate<T>` | `boolean test(T)` | condition |
| `Function<T,R>` | `R apply(T)` | transform |
| `Consumer<T>` | `void accept(T)` | side effect |
| `Supplier<T>` | `T get()` | factory |
| `UnaryOperator<T>` | `T apply(T)` | `Function<T,T>` |
| `BinaryOperator<T>` | `T apply(T,T)` | reduce/combine |
| `BiFunction<T,U,R>` | `R apply(T,U)` | two inputs |
| `BiPredicate`, `BiConsumer` | | two-argument versions |
| `Runnable` | `void run()` | no input, no output |
| `Callable<V>` | `V call() throws` | like Supplier but can throw |

---

## ❓ Q482. What are the primitive specializations and why do they exist?

`IntPredicate`, `IntFunction`, `ToIntFunction`, `IntUnaryOperator`, `IntSupplier`, `IntConsumer`, and the `Long`/`Double` versions.

**Why:** to avoid **boxing**. `Stream<Integer>` allocates an `Integer` per element; `IntStream` does not. On large data this is a big difference. ⚡

---

## ❓ Q483. What default methods do these interfaces provide?

```java
predicate.and(other);  predicate.or(other);  predicate.negate();
Predicate.not(other);                            // Java 11
function.andThen(after);                         // f then g
function.compose(before);                        // g then f
Function.identity();                             // x -> x
consumer.andThen(after);
comparator.reversed().thenComparing(...);
```

---

## ❓ Q484. `andThen` vs `compose`?

```java
f.andThen(g).apply(x)   // g(f(x))  — f first
f.compose(g).apply(x)   // f(g(x))  — g first
```

---

## ❓ Q485. What does `@FunctionalInterface` do?

It is optional documentation **plus a compile-time check**: if you later add a second abstract method, the code fails to compile instead of silently breaking every lambda that used it. Always add it to your own functional interfaces. ✅

---

## ❓ Q486. Do `default` and `static` methods break the SAM rule?

No. Only **abstract** methods count. Also, public methods of `Object` (`equals`, `hashCode`, `toString`) declared in an interface do not count.

---

## ❓ Q487. Write your own functional interface.

```java
@FunctionalInterface
interface TriFunction<A, B, C, R> {
    R apply(A a, B b, C c);
    default <V> TriFunction<A,B,C,V> andThen(Function<? super R, ? extends V> after) {
        return (a, b, c) -> after.apply(apply(a, b, c));
    }
}
```

---

## ❓ Q488. Is `Comparator` a functional interface?

Yes — `compare()` is its single abstract method (`equals` does not count). That is why `Comparator.comparing(Person::getName)` works.

---

## ❓ Q489. What is `Function.identity()` and when do you use it?

`x -> x`. Common in `Collectors.toMap(Function.identity(), ...)` when the element itself is the key.

---

## ❓ Q490. What is currying in Java?

Returning a function from a function:
```java
Function<Integer, Function<Integer, Integer>> add = a -> b -> a + b;
add.apply(2).apply(3);   // 5
```
Rarely used in practice but a good conceptual question.

---

## ❓ Q491. Can a functional interface extend another interface?

Yes, as long as the total number of abstract methods stays one.

---

## ❓ Q492. Why is `Supplier` used for lazy evaluation?

The value is only computed when `get()` is called:
```java
log.debug(() -> expensiveToString());   // only runs if debug is enabled ✅
optional.orElseGet(() -> loadFromDb()); // vs orElse() which ALWAYS evaluates
```

---

# 🌊 Section 3 — Streams (Q493–Q516)

## ❓ Q493. What is a Stream? Is it a data structure? ⭐⭐

**No, it is not a data structure.** It is a pipeline for computing over a source.

| Property | Detail |
|---|---|
| No storage | it does not hold elements |
| **Lazy** | intermediate ops do nothing until a terminal op runs |
| **Single use** | consuming it twice throws `IllegalStateException` |
| Does not modify the source | it produces new results |
| Can be infinite | with `limit()` to bound it |

---

## ❓ Q494. Collection vs Stream? ⭐

| | Collection | Stream |
|---|-----------|--------|
| Purpose | store data | process data |
| Evaluation | eager | **lazy** |
| Traversal | many times | **once** |
| Mutable | yes | no |
| External vs internal iteration | you write the loop | the library iterates |

---

## ❓ Q495. Intermediate vs Terminal operations? ⭐⭐

**Intermediate (return a Stream, lazy):**
`filter`, `map`, `flatMap`, `distinct`, `sorted`, `peek`, `limit`, `skip`, `mapToInt`, `takeWhile`, `dropWhile`

**Terminal (produce a result, trigger execution):**
`forEach`, `collect`, `reduce`, `count`, `min`, `max`, `sum`, `average`, `anyMatch`, `allMatch`, `noneMatch`, `findFirst`, `findAny`, `toArray`, `toList`

> [!warning] Without a terminal operation, **nothing runs**:
> ```java
> list.stream().filter(x -> { System.out.println(x); return true; });  // prints NOTHING
> ```

---

## ❓ Q496. What is lazy evaluation in streams? Show it. ⭐

Elements flow through the whole pipeline **one at a time**, not stage by stage.

```java
Stream.of("a", "b", "c", "d")
    .filter(s -> { System.out.println("filter " + s); return true; })
    .map(s -> { System.out.println("map " + s); return s; })
    .findFirst();
// Output: filter a, map a  — only ONE element processed! ⚡
```
This **short-circuiting** is why streams over large or infinite sources are efficient.

---

## ❓ Q497. How do you create a stream?

```java
list.stream();  list.parallelStream();
Arrays.stream(array);
Stream.of("a", "b");
Stream.iterate(1, x -> x * 2).limit(10);        // infinite + limit
Stream.iterate(1, x -> x < 100, x -> x * 2);    // Java 9: with a predicate
Stream.generate(Math::random).limit(5);
IntStream.range(0, 10);       // 0..9
IntStream.rangeClosed(1, 10); // 1..10
Files.lines(path);            // ⚠️ close it (try-with-resources)
"a,b,c".chars();  Pattern.compile(",").splitAsStream("a,b,c");
Stream.empty();
```

---

## ❓ Q498. `map` vs `flatMap`? ⭐⭐⭐

- `map` → 1 element in, 1 element out (`Stream<Stream<T>>` if the function returns a stream)
- `flatMap` → 1 element in, **N** elements out, all flattened into one stream

```java
List<List<Integer>> nested = List.of(List.of(1,2), List.of(3,4));

nested.stream().map(List::stream);        // Stream<Stream<Integer>> ❌
nested.stream().flatMap(List::stream);    // Stream<Integer> = 1,2,3,4 ✅

// Classic: all words from all sentences
sentences.stream().flatMap(s -> Arrays.stream(s.split(" "))).distinct().toList();
```

---

## ❓ Q499. `findFirst()` vs `findAny()`?

Identical in a sequential stream. In a **parallel** stream, `findAny()` may return any matching element and is faster because it does not need to determine encounter order.

---

## ❓ Q500. `anyMatch` / `allMatch` / `noneMatch` on an empty stream?

- `anyMatch` → **false**
- `allMatch` → **true** ⚠️ (vacuous truth — a classic trap)
- `noneMatch` → **true**

---

## ❓ Q501. What is `reduce()`? Its three forms? ⭐

```java
Optional<T> reduce(BinaryOperator<T> acc);              // no identity → Optional
T reduce(T identity, BinaryOperator<T> acc);            // with identity
U reduce(U identity, BiFunction<U,T,U> acc, BinaryOperator<U> combiner);  // parallel

int sum = nums.stream().reduce(0, Integer::sum);
Optional<String> longest = words.stream().reduce((a,b) -> a.length() > b.length() ? a : b);
```
The **combiner** is only used in parallel streams to merge partial results.

---

## ❓ Q502. What is `peek()` and why is it dangerous?

`peek` is for **debugging** — it observes elements as they pass.

Dangers: it is lazy (does nothing without a terminal op), and the JVM may **skip it entirely** if the pipeline can prove it is unnecessary (e.g. `.peek(...).count()` on a sized stream). Never put business logic in `peek`. ⚠️

---

## ❓ Q503. `limit()` vs `skip()`?

`limit(n)` keeps the first n; `skip(n)` discards the first n. Both are cheap on ordered sequential streams and **expensive on parallel ordered streams**.

---

## ❓ Q504. `takeWhile` vs `dropWhile`? (Java 9)

```java
Stream.of(1,2,3,4,1,2).takeWhile(x -> x < 3);   // 1,2   — stops at the FIRST failure
Stream.of(1,2,3,4,1,2).dropWhile(x -> x < 3);   // 3,4,1,2
```
Different from `filter`, which checks every element.

---

## ❓ Q505. How do you sort with streams?

```java
.sorted()                                          // natural order
.sorted(Comparator.comparing(Person::getName))
.sorted(Comparator.comparingInt(Person::getAge).reversed())
.sorted(Comparator.comparing(Person::getLast).thenComparing(Person::getFirst))
.sorted(Comparator.nullsFirst(Comparator.naturalOrder()))
```

---

## ❓ Q506. What are `IntStream` and friends? ⭐

Primitive streams with no boxing and extra numeric methods:
```java
IntStream.rangeClosed(1, 5).sum();          // 15
list.stream().mapToInt(Person::getAge).average().orElse(0);
IntSummaryStatistics st = ages.summaryStatistics();  // min, max, sum, avg, count ⭐
intStream.boxed().toList();                 // back to Stream<Integer>
```

---

## ❓ Q507. What are parallel streams and when should you use them? ⭐⭐

```java
list.parallelStream().filter(...).collect(...);
```
They split the source using a **Spliterator** and process chunks in the **common ForkJoinPool**.

**Use when ALL of these hold:**
- Large data set (rule of thumb: >10,000 elements)
- CPU-bound work per element
- The source splits well (`ArrayList`, arrays ✅ / `LinkedList`, `Iterator` ❌)
- Operations are **stateless and independent**
- No blocking I/O

**Avoid when:** small data, I/O-bound work, ordered operations like `limit`/`findFirst`, or shared mutable state.

> [!danger] Two real dangers
> 1. **The common pool is shared by the entire JVM** — one blocking parallel stream can starve everything else.
> 2. Overhead often makes parallel **slower** than sequential. Always measure with a real benchmark (JMH), never assume.

---

## ❓ Q508. How do you control the thread pool for a parallel stream?

Submit the stream inside your own ForkJoinPool:
```java
ForkJoinPool pool = new ForkJoinPool(4);
pool.submit(() -> list.parallelStream().map(...).toList()).get();
```
There is no official API — this is a known workaround. 🎩

---

## ❓ Q509. What is a `Spliterator`?

"Splittable iterator" — the engine behind streams. It can `tryAdvance()` one element and `trySplit()` itself in two for parallelism. It also reports characteristics (`SIZED`, `SORTED`, `DISTINCT`, `ORDERED`) that the pipeline uses to optimize.

---

## ❓ Q510. Why must stream operations be stateless and side-effect free? ⭐

```java
List<String> result = new ArrayList<>();
list.parallelStream().forEach(result::add);   // 💥 race condition, ArrayList is not thread-safe
List<String> ok = list.parallelStream().collect(Collectors.toList());   // ✅
```
Use `collect`, not external mutation.

---

## ❓ Q511. What happens if you reuse a stream?

`IllegalStateException: stream has already been operated upon or closed`. Create a new stream from the source, or use a `Supplier<Stream<T>>`.

---

## ❓ Q512. Can you modify the source collection during streaming?

No — same `ConcurrentModificationException` risk as iteration. Streams are also allowed to throw or produce undefined results ("non-interference" requirement).

---

## ❓ Q513. `forEach` vs `forEachOrdered`?

In a parallel stream, `forEach` ignores encounter order (fast); `forEachOrdered` preserves it (slower). In a sequential stream they behave the same.

---

## ❓ Q514. `stream().toList()` vs `collect(Collectors.toList())`? (Java 16)

`toList()` is shorter and returns an **unmodifiable** list. `Collectors.toList()` returns a mutable `ArrayList` (though the API does not guarantee the exact type). Prefer `toList()` unless you need to mutate. ✅

---

## ❓ Q515. How do you handle exceptions inside a stream?

There is no built-in mechanism — wrap in an unchecked exception, or map to a result/`Optional` type:
```java
.map(s -> { try { return parse(s); } catch (Exception e) { return null; } })
.filter(Objects::nonNull)
```

---

## ❓ Q516. Do streams always improve readability?

No. A 6-stage stream with nested lambdas can be far worse than a plain loop. Use streams for **declarative transformation pipelines**; keep loops when you need index access, early exit with complex state, or mutation. Saying this out loud shows judgment, not just knowledge. 🎯

---

# 📥 Section 4 — Collectors (Q517–Q526)

## ❓ Q517. What are the most used collectors? ⭐⭐

```java
Collectors.toList();  toSet();  toUnmodifiableList();
Collectors.toMap(Person::getId, Function.identity());
Collectors.joining(", ", "[", "]");
Collectors.counting();
Collectors.summingInt(Person::getAge);  averagingDouble(...);
Collectors.summarizingInt(Person::getAge);       // stats object
Collectors.groupingBy(Person::getCity);
Collectors.partitioningBy(p -> p.getAge() > 18);
Collectors.mapping(Person::getName, toList());
Collectors.collectingAndThen(toList(), Collections::unmodifiableList);
Collectors.teeing(minBy(...), maxBy(...), (a,b) -> ...);   // Java 12
```

---

## ❓ Q518. `groupingBy` — show the multi-level version. ⭐

```java
// Simple
Map<String, List<Person>> byCity = people.stream()
    .collect(groupingBy(Person::getCity));

// With a downstream collector
Map<String, Long> countByCity = people.stream()
    .collect(groupingBy(Person::getCity, counting()));

// Two levels
Map<String, Map<Integer, List<Person>>> byCityThenAge = people.stream()
    .collect(groupingBy(Person::getCity, groupingBy(Person::getAge)));

// Custom map type + downstream
Map<String, Set<String>> namesByCity = people.stream()
    .collect(groupingBy(Person::getCity, TreeMap::new,
                        mapping(Person::getName, toSet())));
```

---

## ❓ Q519. `groupingBy` vs `partitioningBy`?

`partitioningBy` always produces exactly **two** entries with `Boolean` keys (`true` and `false`) — even if one is empty. `groupingBy` produces one entry per distinct key.

---

## ❓ Q520. What is the `toMap` duplicate-key trap? ⭐

```java
.collect(toMap(Person::getName, Person::getAge));
// 💥 IllegalStateException: Duplicate key

// ✅ provide a merge function
.collect(toMap(Person::getName, Person::getAge, (a, b) -> a));

// ✅ and a map supplier if you need ordering
.collect(toMap(k, v, (a,b) -> a, LinkedHashMap::new));
```

> [!warning] Second trap: `toMap` throws **NPE** if a **value** is null (unlike `HashMap.put`).

---

## ❓ Q521. How do you write a custom collector?

```java
Collector.of(
    ArrayList::new,           // supplier
    List::add,                // accumulator
    (a, b) -> { a.addAll(b); return a; },   // combiner (parallel)
    Collector.Characteristics.IDENTITY_FINISH);
```
Rarely needed — usually `collectingAndThen` or `reducing` is enough.

---

## ❓ Q522. `reduce` vs `collect`? ⭐

- `reduce` → **immutable** reduction; each step produces a new value. Bad for strings (`O(n²)` concatenation).
- `collect` → **mutable** reduction into a container. This is why `Collectors.joining()` beats `reduce(String::concat)`.

---

## ❓ Q523. What is `flatMapping` and `filtering`? (Java 9)

Downstream collectors that let you filter/flatten **inside** a `groupingBy` without losing empty groups:
```java
groupingBy(Person::getCity, filtering(p -> p.getAge() > 18, toList()))
```
Different from filtering before grouping, which drops the key entirely.

---

## ❓ Q524. How do you compute statistics in one pass?

```java
IntSummaryStatistics stats = people.stream().collect(summarizingInt(Person::getAge));
stats.getMin(); stats.getMax(); stats.getAverage(); stats.getSum(); stats.getCount();
```

---

## ❓ Q525. How do you join strings?

```java
names.stream().collect(joining(", "));           // "a, b, c"
String.join(", ", names);                        // simpler when you already have a Collection ✅
```

---

## ❓ Q526. What are common stream one-liners worth memorizing? ⭐

```java
// Word frequency
Map<String,Long> freq = words.stream().collect(groupingBy(w -> w, counting()));

// Top 3 by value
map.entrySet().stream().sorted(Map.Entry.<K,V>comparingByValue().reversed()).limit(3).toList();

// Remove duplicates keeping order
list.stream().distinct().toList();

// Find duplicates
list.stream().filter(x -> !seen.add(x)).collect(toSet());

// Sum of a field
orders.stream().mapToDouble(Order::getTotal).sum();

// Group and count
people.stream().collect(groupingBy(Person::getCity, counting()));

// Flatten
lists.stream().flatMap(List::stream).toList();

// Max by field
people.stream().max(comparingInt(Person::getAge));

// Convert list to map safely
people.stream().collect(toMap(Person::getId, identity(), (a,b) -> a));
```

---

# 🎁 Section 5 — Optional (Q527–Q536)

## ❓ Q527. What is `Optional` and what problem does it solve? ⭐

A container that may or may not hold a non-null value. It makes "there may be no result" **explicit in the type signature** instead of a surprise NPE.

```java
Optional<User> findById(String id);   // the caller cannot ignore the empty case
```

---

## ❓ Q528. How do you create and use an Optional?

```java
Optional.of(value);              // throws NPE if value is null
Optional.ofNullable(maybeNull);  // safe ✅
Optional.empty();

opt.isPresent();  opt.isEmpty();          // isEmpty is Java 11
opt.get();                                // ⚠️ throws if empty — avoid
opt.orElse("default");                    // eager
opt.orElseGet(() -> expensive());         // lazy ✅
opt.orElseThrow(() -> new NotFoundException());
opt.ifPresent(v -> print(v));
opt.ifPresentOrElse(v -> print(v), () -> print("none"));   // Java 9
opt.map(User::getName).filter(n -> !n.isBlank()).orElse("anon");
opt.flatMap(User::getAddressOptional);
opt.or(() -> Optional.of(fallback));      // Java 9
opt.stream();                             // Java 9 — 0 or 1 element
```

---

## ❓ Q529. `orElse` vs `orElseGet`? ⭐ (common trap)

```java
opt.orElse(expensiveCall());       // ⚠️ expensiveCall() ALWAYS runs, even if present
opt.orElseGet(() -> expensiveCall());  // ✅ runs only when empty
```

---

## ❓ Q530. What are Optional anti-patterns? ⭐⭐

```java
if (opt.isPresent()) { use(opt.get()); }   // ❌ just a null check with extra steps
opt.ifPresent(this::use);                  // ✅

Optional<List<X>> list;                    // ❌ return an empty list instead
private Optional<String> field;            // ❌ never use as a FIELD (not Serializable)
void m(Optional<String> arg);              // ❌ never as a PARAMETER — overload instead
return Optional.ofNullable(x).orElse(null);// ❌ pointless round trip
Optional.of(mightBeNull);                  // ❌ throws NPE
```

**Optional's intended use is a RETURN type.** That is what it was designed for. ✅

---

## ❓ Q531. Is `Optional` serializable?

**No.** That is one reason it should not be a field in an entity or DTO.

---

## ❓ Q532. `map` vs `flatMap` on Optional?

If the function returns a plain value → `map`. If it already returns an `Optional` → `flatMap` (otherwise you get `Optional<Optional<T>>`).

---

## ❓ Q533. What are `OptionalInt`, `OptionalDouble`?

Primitive versions returned by `IntStream.max()`, `average()`, etc. — they avoid boxing but have no `map`/`filter`.

---

## ❓ Q534. Does Optional prevent all NPEs?

No — you can still hold `Optional` itself as null, and `get()` on empty throws `NoSuchElementException`. It is a **design signal**, not a runtime guard.

---

## ❓ Q535. How does Optional chain nicely?

```java
String city = Optional.ofNullable(user)
    .map(User::getAddress)
    .map(Address::getCity)
    .map(String::toUpperCase)
    .orElse("UNKNOWN");
```
This replaces four nested null checks with one readable chain. ✨

---

## ❓ Q536. How do you use Optional with streams?

```java
// Java 9+: drop empties elegantly
List<String> names = users.stream()
    .map(User::findNickname)    // Stream<Optional<String>>
    .flatMap(Optional::stream)  // ⭐ Stream<String>, empties disappear
    .toList();
```

---

# 📅 Section 6 — Date/Time API (Q537–Q544)

## ❓ Q537. What was wrong with `Date` and `Calendar`? ⭐

- **Mutable** → not thread-safe
- `Date` months are 0-based, years offset from 1900 😵
- `SimpleDateFormat` is **not thread-safe** (a classic production bug)
- Poor time zone handling, no separation of date vs time vs instant

---

## ❓ Q538. What are the main `java.time` classes? ⭐

| Class | Represents |
|---|---|
| `LocalDate` | date only (2026-08-11) |
| `LocalTime` | time only (14:30) |
| `LocalDateTime` | date + time, **no zone** |
| `ZonedDateTime` | date + time + zone |
| `OffsetDateTime` | date + time + UTC offset (best for APIs/DB) |
| `Instant` | a point on the UTC timeline (machine time) |
| `Duration` | time-based amount (seconds/nanos) |
| `Period` | date-based amount (years/months/days) |
| `DateTimeFormatter` | **immutable and thread-safe** ✅ |

---

## ❓ Q539. Show common operations.

```java
LocalDate today = LocalDate.now();
LocalDate d = LocalDate.of(2026, Month.AUGUST, 11);
LocalDate next = today.plusDays(7).minusMonths(1).withDayOfMonth(1);
boolean before = d.isBefore(today);
long days = ChronoUnit.DAYS.between(d, today);
Period p = Period.between(birthday, today);      // years/months/days
LocalDate lastDay = today.with(TemporalAdjusters.lastDayOfMonth());
String s = today.format(DateTimeFormatter.ofPattern("dd/MM/yyyy"));
LocalDate parsed = LocalDate.parse("2026-08-11");
```

---

## ❓ Q540. Why is `java.time` immutable?

Every operation returns a **new** object, making all classes thread-safe and eliminating the aliasing bugs of `Calendar`.

```java
date.plusDays(1);          // ⚠️ result discarded — must reassign
date = date.plusDays(1);   // ✅
```

---

## ❓ Q541. `Duration` vs `Period`?

`Duration` = machine time (seconds, nanos) — use with `Instant`/`LocalTime`.
`Period` = human time (years, months, days) — use with `LocalDate`, and it respects varying month lengths and DST.

---

## ❓ Q542. What should you store in a database?

Usually **`Instant`/UTC timestamps** for events, and `LocalDate` for calendar concepts like a birthday. Store the zone separately if the user's local time matters.

---

## ❓ Q543. How do you convert between old and new APIs?

```java
Instant i = date.toInstant();
Date d = Date.from(instant);
LocalDateTime ldt = instant.atZone(ZoneId.systemDefault()).toLocalDateTime();
```

---

## ❓ Q544. Why is `SimpleDateFormat` dangerous?

It keeps mutable internal state (`Calendar`), so sharing one static instance across threads silently produces **wrong dates**. Either create a new instance per use, use `ThreadLocal`, or — best — use `DateTimeFormatter`. ✅

---

# 🆕 Section 7 — Java 9 to 21 Features (Q545–Q556)

## ❓ Q545. What are the notable features by version? ⭐

| Version | Highlights |
|---|---|
| **8** (LTS) | lambdas, streams, `Optional`, `java.time`, default methods |
| **9** | modules (JPMS), `List.of()`, private interface methods, `var`-free JShell |
| **10** | `var` (local type inference) |
| **11** (LTS) | `HttpClient`, `String` methods (`isBlank`, `strip`, `repeat`, `lines`), single-file source launch, `var` in lambdas |
| **14** | switch expressions, helpful NPEs, records (preview) |
| **15** | text blocks |
| **16** | **records**, pattern matching for `instanceof` |
| **17** (LTS) | **sealed classes**, enhanced pseudo-random |
| **21** (LTS) | **virtual threads**, pattern matching for `switch`, record patterns, sequenced collections |

---

## ❓ Q546. What are switch expressions? (Java 14)

```java
int len = switch (day) {
    case MON, TUE -> 1;
    case WED -> { int x = compute(); yield x; }
    default -> 0;
};
```
No fall-through, returns a value, and must be **exhaustive** for enums.

---

## ❓ Q547. What is pattern matching for `instanceof`? (Java 16)

```java
if (obj instanceof String s && s.length() > 5) {   // s is in scope and typed ✅
    System.out.println(s.toUpperCase());
}
```
No cast needed. The scope is flow-sensitive.

---

## ❓ Q548. What is pattern matching for `switch` + record patterns? (Java 21) ⭐

```java
String describe(Object o) {
    return switch (o) {
        case Integer i when i > 100 -> "big number";     // guarded pattern
        case Integer i              -> "number " + i;
        case Point(int x, int y)    -> "point " + x + "," + y;   // record pattern ⭐
        case null                   -> "nothing";
        default                     -> "unknown";
    };
}
```
Combined with `sealed` interfaces, the compiler can verify exhaustiveness.

---

## ❓ Q549. What are sequenced collections? (Java 21)

New interfaces `SequencedCollection`, `SequencedSet`, `SequencedMap` giving uniform `getFirst()`, `getLast()`, `addFirst()`, `reversed()` to `List`, `Deque`, `LinkedHashSet`, `LinkedHashMap`, and `SortedMap`. Finally consistent. ✅

---

## ❓ Q550. What is the new `HttpClient`? (Java 11)

```java
HttpClient client = HttpClient.newHttpClient();
HttpResponse<String> r = client.send(
    HttpRequest.newBuilder(URI.create(url)).GET().build(),
    HttpResponse.BodyHandlers.ofString());
client.sendAsync(request, handler).thenApply(HttpResponse::body);
```
Supports HTTP/2, WebSocket, and async via `CompletableFuture`.

---

## ❓ Q551. What are the useful Java 11 String methods?

```java
"  ".isBlank();  " x ".strip();  "ab".repeat(3);
"a\nb".lines().toList();
"%s".formatted(x);        // Java 15
"a".stripLeading();  "a".stripTrailing();
```

---

## ❓ Q552. What is JShell?

The official REPL (`jshell`) for trying snippets without a class or `main` — great for interview whiteboarding and learning.

---

## ❓ Q553. What is the difference between LTS and non-LTS releases?

Java releases every 6 months; LTS versions (8, 11, 17, 21, 25) get years of updates. Most companies run an LTS. Knowing that 21 is the current common LTS target signals you follow the ecosystem. 📅

---

## ❓ Q554. What is `var` in lambda parameters? (Java 11)

`(var x, var y) -> x + y` — useful only to attach annotations like `(@NonNull var x) -> ...`.

---

## ❓ Q555. What are text blocks used for?

Multi-line strings without escaping — SQL, JSON, HTML. Incidental indentation is stripped automatically.

---

## ❓ Q556. What is coming next in Java?

[Guessing — this moves fast, verify before an interview] Project **Valhalla** (value types / primitive classes), **Loom** follow-ups (structured concurrency), **Panama** (foreign function & memory API), and **Amber** (continued language ergonomics). Naming these projects shows genuine ecosystem awareness.

---

# 🧩 Section 8 — Quick Fire Round

> [!question]- Can you reuse a stream?
> No — `IllegalStateException`.

> [!question]- Does `filter` run without a terminal operation?
> No. Intermediate operations are lazy.

> [!question]- What does `allMatch` return on an empty stream?
> `true`.

> [!question]- Is `parallelStream()` always faster?
> No — often slower for small data or I/O work.

> [!question]- Which pool do parallel streams use?
> The shared `ForkJoinPool.commonPool()`.

> [!question]- What is the SAM rule?
> Single Abstract Method — the requirement for a functional interface.

> [!question]- Difference between `Collection.stream()` and `Collection.parallelStream()`?
> Sequential vs parallel execution of the same pipeline.

> [!question]- Should `Optional` be a method parameter?
> No — use overloading or accept null with clear documentation.

> [!question]- Which is lazy: `orElse` or `orElseGet`?
> `orElseGet`.

> [!question]- Is `DateTimeFormatter` thread-safe?
> Yes — unlike `SimpleDateFormat`.

> [!question]- What does `flatMap(Optional::stream)` do?
> Removes empty Optionals from a stream (Java 9).

> [!question]- What replaced `Date`/`Calendar`?
> The `java.time` package (JSR-310), inspired by Joda-Time.

---

## 🎓 Self-Test Checklist for Part 7

- [ ] I can explain lambda capture and effectively-final
- [ ] I know the 6 core functional interfaces and their methods by heart
- [ ] I can explain laziness with the `findFirst` example
- [ ] I can explain `map` vs `flatMap` with a concrete case
- [ ] I can list 5 conditions for parallel streams to actually help
- [ ] I can write multi-level `groupingBy` from memory
- [ ] I know the `toMap` duplicate-key and null-value traps
- [ ] I can list 5 Optional anti-patterns
- [ ] I know why `SimpleDateFormat` is dangerous

---

> [!success] ✅ Part 7 complete — Q469–Q556
> 👉 Next: [[01 - Java/Interview/08 - IO & Reflection|Part 8 — IO & Reflection]]

#java #interview #core-java #java8 #streams #part7
