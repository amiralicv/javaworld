---
type: interview
series: Java Interview
part: 3
tags: [java, interview]
---

# 📦 Java Core Interview Reference — Part 3: Collections Framework

> [!info] About this note
> **Part 3 of 9** — Collections Framework (the most asked topic in Java interviews)
> Format: Question ➜ Short answer ➜ Deep answer ➜ Code ➜ Interview trap
> Previous: [[01 - Java/Interview/02 - OOP|Part 2 — OOP]]
> Tags: #java #interview #core-java #collections

---

## 🗺️ Series Map

| Part | Topic | Status |
|------|-------|--------|
| 1 | ☕ Language Basics & Fundamentals | ✅ |
| 2 | 🧬 OOP Deep Dive | ✅ |
| **3** | 📦 Collections Framework | ✅ You are here |
| 4 | ⚠️ Exceptions & Generics | ⏳ |
| 5 | 🧵 Multithreading & Concurrency | ⏳ |
| 6 | 🧠 JVM Memory, GC & Class Loading | ⏳ |
| 7 | 🚀 Java 8+ (Lambda, Stream, Optional) | ⏳ |
| 8 | 💾 I/O, Serialization, Reflection, Annotations | ⏳ |
| 9 | 🎯 Design Patterns + Tricky Output Puzzles | ⏳ |

---

## 📑 Table of Contents

- [[#🌳 Section 1 — Hierarchy & Fundamentals (Q155–Q164)]]
- [[#📋 Section 2 — List Family (Q165–Q178)]]
- [[#🗺️ Section 3 — HashMap Internals ⭐ THE BIG ONE (Q179–Q196)]]
- [[#🔑 Section 4 — Other Map Implementations (Q197–Q208)]]
- [[#🎯 Section 5 — Set Family (Q209–Q216)]]
- [[#🚦 Section 6 — Queue, Deque & PriorityQueue (Q217–Q224)]]
- [[#🔄 Section 7 — Iterator, Fail-Fast & CME (Q225–Q232)]]
- [[#🛠️ Section 8 — Collections Utility & Immutable Collections (Q233–Q240)]]
- [[#⚡ Section 9 — Big-O Performance Cheat Sheet]]
- [[#🧩 Section 10 — Quick Fire Round]]

---

# 🌳 Section 1 — Hierarchy & Fundamentals (Q155–Q164)

## ❓ Q155. Draw the Collections Framework hierarchy. ⭐⭐

```
                    Iterable (interface)
                        │
                   Collection
        ┌───────────────┼───────────────┐
       List            Set            Queue
        │               │               │
  ┌─────┼─────┐    ┌────┼────┐     ┌────┴─────┐
ArrayList  Vector  HashSet  SortedSet    Deque  PriorityQueue
LinkedList   │       │      (TreeSet)      │
          Stack  LinkedHashSet        ArrayDeque
                                      LinkedList

                    Map  (⚠️ NOT a Collection!)
        ┌───────────┬─────┴──────┬──────────────┐
    HashMap     Hashtable     SortedMap    ConcurrentHashMap
       │            │         (TreeMap)
 LinkedHashMap  Properties
```

> [!warning] The #1 fact people forget
> **`Map` does not extend `Collection`.** A Collection holds single elements; a Map holds key→value pairs. They are separate hierarchies, connected only through `map.entrySet()`, `keySet()`, `values()`.

---

## ❓ Q156. What is the Collections Framework and why does it exist?

A unified architecture of interfaces + implementations + algorithms for storing groups of objects.

**Benefits:** less code to write, tested/optimized data structures, interoperability (any `List` works everywhere a `List` is expected), and reusable algorithms (`sort`, `binarySearch`, `reverse`).

---

## ❓ Q157. `Collection` vs `Collections`?

- **`Collection`** = root **interface** (`java.util.Collection`)
- **`Collections`** = **utility class** with static methods (`sort`, `unmodifiableList`, `synchronizedList`, `emptyList`, `reverse`, `shuffle`)

Similarly: `Array` (no such class for utilities) vs **`Arrays`** (utility class).

---

## ❓ Q158. Main differences: List vs Set vs Map vs Queue? ⭐

| | **List** | **Set** | **Map** | **Queue** |
|---|---------|---------|---------|-----------|
| Duplicates | ✅ allowed | ❌ unique | keys ❌, values ✅ | ✅ allowed |
| Order | ✅ insertion order, indexed | depends on impl | depends on impl | FIFO / priority |
| Null | multiple nulls | one null (HashSet) | 1 null key (HashMap) | ❌ usually not |
| Access | by index | no index | by key | head only |

---

## ❓ Q159. Which collections allow `null`? ⭐

| Collection | Null allowed? |
|---|---|
| `ArrayList`, `LinkedList`, `Vector` | ✅ many |
| `HashSet`, `LinkedHashSet` | ✅ one |
| `TreeSet` | ❌ `NullPointerException` (needs comparison) |
| `HashMap` | ✅ **one null key**, many null values |
| `LinkedHashMap` | ✅ same as HashMap |
| `TreeMap` | ❌ null key, ✅ null values |
| `Hashtable` | ❌ neither key nor value |
| `ConcurrentHashMap` | ❌ neither |
| `ArrayDeque`, `PriorityQueue` | ❌ |
| `List.of(...)`, `Map.of(...)` | ❌ |

> [!tip] Why does `ConcurrentHashMap` forbid null? Because `map.get(k) == null` would be ambiguous: "absent" or "mapped to null"? In a single-threaded `HashMap` you can call `containsKey()` to disambiguate; in a concurrent map that check is racy.

---

## ❓ Q160. Which classes are synchronized (legacy thread-safe)?

`Vector`, `Stack`, `Hashtable`, `Properties`. They synchronize **every method**, which is slow and still **not** safe for compound operations.

Modern replacements → `ConcurrentHashMap`, `CopyOnWriteArrayList`, `ConcurrentLinkedQueue`. Details in [[01 - Java/Interview/05 - Concurrency|Part 5 — Concurrency]].

---

## ❓ Q161. How do you make a collection thread-safe?

```java
List<String> sync = Collections.synchronizedList(new ArrayList<>());

// ⚠️ Iteration still needs a manual lock:
synchronized (sync) {
    for (String s : sync) { ... }
}
```
Better: use `java.util.concurrent` classes designed for it.

---

## ❓ Q162. `Iterable` vs `Iterator`?

- **`Iterable`** — "I can be looped over". One method: `iterator()`. Enables the for-each loop.
- **`Iterator`** — the cursor itself: `hasNext()`, `next()`, `remove()`.

```java
class Bag implements Iterable<String> {
    public Iterator<String> iterator() { return list.iterator(); }
}
for (String s : bag) { }   // works because Bag is Iterable ✅
```

---

## ❓ Q163. What is the initial capacity and load factor?

- **Capacity** = number of buckets/slots allocated
- **Load factor** = how full before resizing (default `0.75`)
- **Threshold** = capacity × load factor → resize when exceeded

`ArrayList` default capacity **10** (lazily created), `HashMap` default **16**.

---

## ❓ Q164. Why is `0.75` the default load factor? ⭐

It is a **time–space trade-off**:
- Lower (e.g. 0.5) → fewer collisions, faster lookups, but wasted memory
- Higher (e.g. 1.0) → less memory, more collisions, slower lookups

0.75 is empirically balanced; with a good hash the number of entries per bucket follows a Poisson distribution where collisions stay rare. [Likely] This exact reasoning is documented in the `HashMap` source comments.

---

# 📋 Section 2 — List Family (Q165–Q178)

## ❓ Q165. `ArrayList` vs `LinkedList`? ⭐⭐⭐ (asked constantly)

| Operation | `ArrayList` | `LinkedList` |
|-----------|-------------|--------------|
| Internal | dynamic **array** | **doubly linked list** |
| `get(i)` | **O(1)** ⚡ | O(n) 🐢 |
| `add()` at end | O(1) amortized | O(1) |
| `add/remove` at **start** | O(n) | **O(1)** ⚡ |
| `add/remove` in middle | O(n) shift | O(n) search + O(1) unlink |
| Memory | compact | +2 pointers per node (~24 bytes overhead) |
| Cache locality | ✅ excellent | ❌ poor (scattered nodes) |
| Implements | `List`, `RandomAccess` | `List`, `Deque` |

> [!danger] The honest real-world answer that impresses seniors
> "In practice I almost always use `ArrayList`. `LinkedList` wins on paper for head insertion, but its poor CPU cache locality makes it slower in real benchmarks for most workloads. The only common case for `LinkedList` is when I need a `Deque` — and even then `ArrayDeque` is faster."

---

## ❓ Q166. How does `ArrayList` grow internally? ⭐

1. Default capacity **10** (created lazily on first `add`)
2. When `size == capacity` → `grow()` is called
3. New capacity = `oldCapacity + (oldCapacity >> 1)` = **1.5×**
4. `Arrays.copyOf()` copies the old array into the new one

```
10 → 15 → 22 → 33 → 49 → 73 ...
```

**Cost:** each resize is O(n), but it happens rarely → **amortized O(1)** for `add()`.

> [!tip] Optimization: if you know the size, pre-allocate: `new ArrayList<>(10000)` — avoids many copies.

---

## ❓ Q167. `ArrayList` vs `Vector`? ⭐

| | `ArrayList` | `Vector` |
|---|-------------|----------|
| Sync | ❌ not synchronized | ✅ every method synchronized |
| Speed | fast | slow (lock overhead) |
| Growth | **1.5×** | **2×** (doubles) |
| Since | 1.2 | 1.0 (legacy) |
| Iterator | fail-fast | fail-fast (`Enumeration` is not) |

**Use `Vector`?** Never in new code.

---

## ❓ Q168. What is `CopyOnWriteArrayList`?

A thread-safe list where **every write creates a fresh copy** of the internal array.

- ✅ Reads are lock-free and very fast
- ✅ Iterators never throw `ConcurrentModificationException` (they see a snapshot)
- ❌ Writes are O(n) and expensive

**Use when:** many reads, very few writes — e.g. a listener/observer registry.

---

## ❓ Q169. How do you remove elements while iterating? ⭐⭐

```java
List<String> list = new ArrayList<>(List.of("a", "b", "c"));

// ❌ throws ConcurrentModificationException
for (String s : list) if (s.equals("b")) list.remove(s);

// ✅ 1. Iterator.remove()
Iterator<String> it = list.iterator();
while (it.hasNext()) if (it.next().equals("b")) it.remove();

// ✅ 2. removeIf (Java 8) — cleanest
list.removeIf(s -> s.equals("b"));

// ✅ 3. classic reverse index loop
for (int i = list.size() - 1; i >= 0; i--)
    if (list.get(i).equals("b")) list.remove(i);
```

---

## ❓ Q170. `remove(int)` vs `remove(Object)` — the overload trap ⭐

```java
List<Integer> list = new ArrayList<>(List.of(10, 20, 30));
list.remove(1);                      // removes INDEX 1 → 20 removed
list.remove(Integer.valueOf(10));    // removes the OBJECT 10 ✅
```
For a `List<Integer>` this bites everyone. The `int` overload wins because exact match beats boxing.

---

## ❓ Q171. What does `Arrays.asList()` return? What are its traps? ⭐

It returns a **fixed-size** list **backed by the original array** — not an `ArrayList`.

```java
List<String> list = Arrays.asList("a", "b");
list.set(0, "z");   // ✅ allowed — writes through to the array
list.add("c");      // ❌ UnsupportedOperationException
list.remove(0);     // ❌ UnsupportedOperationException
```

**Primitive trap:**
```java
int[] arr = {1, 2, 3};
List<int[]> wrong = Arrays.asList(arr);       // size 1! one int[] element 😱
List<Integer> right = Arrays.stream(arr).boxed().toList();   // ✅
```

**To get a real modifiable list:** `new ArrayList<>(Arrays.asList("a","b"))`

---

## ❓ Q172. `List.of()` vs `Arrays.asList()` vs `new ArrayList<>()`?

| | `List.of()` (J9) | `Arrays.asList()` | `new ArrayList<>()` |
|---|---|---|---|
| Mutable | ❌ fully immutable | ⚠️ fixed-size, `set` allowed | ✅ fully |
| Nulls | ❌ NPE | ✅ allowed | ✅ |
| Backed by array | copy | the original array | own array |

---

## ❓ Q173. How do you convert between arrays and lists?

```java
// Array → List
List<String> l1 = Arrays.asList(arr);              // fixed size
List<String> l2 = new ArrayList<>(Arrays.asList(arr));  // modifiable
List<String> l3 = Arrays.stream(arr).toList();     // Java 16, immutable

// List → Array
String[] a1 = list.toArray(new String[0]);         // ✅ preferred idiom
Object[] a2 = list.toArray();                      // loses type
String[] a3 = list.toArray(String[]::new);         // Java 11 ✅
```

---

## ❓ Q174. What is `RandomAccess`?

A **marker interface** implemented by `ArrayList` and `Vector` saying "index access is fast". Algorithms in `Collections` check it and choose an index loop vs an iterator loop accordingly.

```java
if (list instanceof RandomAccess) { /* use for(i) */ } else { /* use iterator */ }
```

---

## ❓ Q175. How does `Collections.sort()` / `List.sort()` work internally?

It uses **TimSort** (a hybrid of merge sort and insertion sort) for objects — stable, adaptive, O(n log n) worst case, O(n) on already-sorted data.

For **primitives**, `Arrays.sort()` uses **dual-pivot QuickSort** — faster but not stable (stability does not matter for primitives).

> [!tip] Why the difference? Stability matters for objects (you may sort by name, then by age, and want the first order preserved). Merge sort needs extra memory but is stable.

---

## ❓ Q176. What is a stable sort?

Equal elements keep their original relative order. TimSort ✅, QuickSort ❌.

---

## ❓ Q177. What is `subList()` and its danger?

`list.subList(1, 3)` returns a **view**, not a copy. Changing the view changes the original — and structurally modifying the original invalidates the view (`ConcurrentModificationException`).

```java
List<Integer> sub = list.subList(0, 3);
sub.clear();   // 💥 removes those elements from the ORIGINAL list too
```

---

## ❓ Q178. What is `Stack` and what should we use instead?

`Stack extends Vector` — a design mistake (see Part 2, Q76): it exposes `add(index, e)` and is synchronized.

**Use `ArrayDeque` instead:**
```java
Deque<Integer> stack = new ArrayDeque<>();
stack.push(1); stack.pop(); stack.peek();
```

---

# 🗺️ Section 3 — HashMap Internals ⭐ THE BIG ONE (Q179–Q196)

> [!danger] If you learn only one section in this whole series, make it this one.

## ❓ Q179. How does `HashMap` work internally? ⭐⭐⭐ (the classic)

**The 60-second answer:**

`HashMap` stores entries in an **array of buckets** (`Node<K,V>[] table`). Each `Node` holds `hash`, `key`, `value`, `next`.

**On `put(key, value)`:**
1. Compute `key.hashCode()`
2. **Spread** it: `h = hash ^ (hash >>> 16)` (mixes high bits into low bits)
3. Find the bucket: `index = (n - 1) & hash` (works because `n` is a power of 2 — equal to `hash % n` but much faster)
4. If the bucket is **empty** → place the new Node
5. If **occupied** (collision) → walk the chain:
   - if a node has the **same hash AND (`==` or `equals`)** → **replace** the value
   - else append to the end of the linked list
6. If the chain length reaches **8** and table size ≥ **64** → convert the list into a **red-black tree** 🌳
7. If `size > capacity × 0.75` → **resize** (double the table and rehash)

**On `get(key)`:** same hash → same bucket → compare with `equals()` → return the value or `null`.

```
table[]
 0 →  null
 1 →  [Node A] → [Node B] → [Node C]      ← collision chain
 2 →  null
 3 →  [Node D]
 ...
15 →  [ Red-Black Tree ]                  ← after 8+ collisions
```

---

## ❓ Q180. Why is capacity always a power of 2? ⭐

Because then `index = (n - 1) & hash` is equivalent to `hash % n` but uses a **single AND instruction** instead of an expensive modulo. `n-1` gives a mask of all 1 bits (e.g. 16-1 = `1111`).

If you pass a non-power-of-2 to the constructor, `HashMap` rounds **up** to the next power of 2 (`tableSizeFor`).

---

## ❓ Q181. What is the hash spreading function and why is it needed?

```java
static int hash(Object key) {
    int h;
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```

Because the index uses only the **low bits** of the hash, two keys differing only in high bits would collide. XOR-ing the top 16 bits down mixes them in — cheap but effective. 🎲

---

## ❓ Q182. What happens on a hash collision?

Two keys land in the same bucket. They are stored in a **linked list** (Java 7: at the head; Java 8: at the tail) and compared one by one using `hashCode` then `equals`.

Java 8 upgrade: if one bucket's chain grows to **8** nodes **and** the table has at least **64** buckets, the chain becomes a **red-black tree** → worst case improves from **O(n)** to **O(log n)**. 🌳

If the tree shrinks back to **6** nodes, it un-treeifies into a list.

---

## ❓ Q183. Why 8 for treeify and 6 for untreeify? Why not 7 and 7?

The gap prevents **thrashing** — constant conversion back and forth when the size oscillates around the threshold. 8 was chosen because with a good hash, the probability of a bucket reaching 8 elements is around 0.00000006 (Poisson) — so trees should be extremely rare in healthy maps. [Certain] These numbers are documented in the JDK source.

---

## ❓ Q184. What happens during `HashMap` resize? ⭐

1. New table with **double** the capacity
2. Every entry is redistributed

**Java 8 clever trick:** since capacity doubles, an entry either stays at index `i` or moves to `i + oldCapacity` — determined by a single bit check `(hash & oldCap) == 0`. No rehashing needed, and the split preserves relative order (which is why Java 8 fixed the infinite loop bug).

**Cost:** O(n). Pre-size your map to avoid it: `new HashMap<>(expectedSize / 0.75 + 1)`.

---

## ❓ Q185. What was the infinite loop bug in Java 7 `HashMap`? ⭐

In Java 7, resizing under concurrent access could create a **circular linked list** in a bucket, because entries were re-inserted at the **head** (order reversed). A later `get()` would loop forever → **100% CPU** on a production server. 🔥

Java 8 appends at the **tail** and preserves order during split → the infinite loop is gone. But **`HashMap` is still not thread-safe** — you can still lose updates and get corrupted state. Use `ConcurrentHashMap`.

---

## ❓ Q186. Can `HashMap` have a null key? How is it stored?

**Yes, exactly one.** Its hash is defined as `0`, so it always lands in **bucket 0**. Null values are unlimited.

---

## ❓ Q187. What happens if two keys have the same `hashCode` but are not `equals`?

Both are stored in the **same bucket** as separate entries in the chain. Lookups still work correctly — just slower.

---

## ❓ Q188. What if you use a mutable object as a key? ⭐

The entry becomes **unreachable**:

```java
Map<List<String>, String> map = new HashMap<>();
List<String> key = new ArrayList<>(List.of("a"));
map.put(key, "value");
key.add("b");                 // hash changed!
map.get(key);                 // null 😱 — searched in the wrong bucket
```

> [!tip] Rule: **keys must be immutable** (or at least their `hashCode` must never change). That is why `String` is the perfect key.

---

## ❓ Q189. What if a key's class does not override `hashCode()`?

It uses `Object.hashCode()` = identity hash. Two logically equal objects get different hashes → you can never look up with a new instance:

```java
map.put(new Point(1,1), "a");
map.get(new Point(1,1));   // null ❌ without hashCode/equals
```

---

## ❓ Q190. Time complexity of `HashMap` operations?

| Case | get/put/remove |
|------|----------------|
| Average | **O(1)** ⚡ |
| Worst (all collide, list) | O(n) |
| Worst (Java 8 tree) | **O(log n)** |

---

## ❓ Q191. `HashMap` vs `Hashtable`? ⭐⭐

| | `HashMap` | `Hashtable` |
|---|-----------|-------------|
| Sync | ❌ | ✅ every method |
| Null key/value | ✅ 1 key, many values | ❌ NPE |
| Performance | fast | slow |
| Iteration | `Iterator` (fail-fast) | `Enumeration` (not fail-fast) + Iterator |
| Since | 1.2 | 1.0 (legacy) |
| Extends | `AbstractMap` | `Dictionary` |
| Initial capacity / growth | 16 / ×2 | 11 / ×2+1 |

---

## ❓ Q192. `HashMap` vs `ConcurrentHashMap`? ⭐⭐

| | `HashMap` | `ConcurrentHashMap` |
|---|-----------|---------------------|
| Thread safe | ❌ | ✅ |
| Locking | none | **per-bucket** (`synchronized` on the head node) + CAS |
| Null | allowed | ❌ NPE |
| Iterator | fail-fast (CME) | **weakly consistent**, no CME |
| Read performance | fastest | almost as fast (reads are lock-free via `volatile`) |

**Java 7 vs 8:** Java 7 used **segment locking** (16 segments = 16 concurrent writers max). Java 8 dropped segments for **CAS + synchronized on the first node of each bucket** → concurrency level = number of buckets. 🚀

---

## ❓ Q193. What are the useful Java 8 `Map` methods? ⭐

```java
map.getOrDefault(key, 0);
map.putIfAbsent(key, value);
map.computeIfAbsent(key, k -> new ArrayList<>()).add(item);   // ⭐ multimap idiom
map.computeIfPresent(key, (k, v) -> v + 1);
map.compute(key, (k, v) -> v == null ? 1 : v + 1);
map.merge(key, 1, Integer::sum);                              // ⭐ word count idiom
map.forEach((k, v) -> System.out.println(k + "=" + v));
map.replaceAll((k, v) -> v.toUpperCase());
map.entrySet().removeIf(e -> e.getValue() == null);
```

**Word count in one line:**
```java
for (String w : words) counts.merge(w, 1, Integer::sum);
```

---

## ❓ Q194. How do you iterate over a Map? Which way is fastest?

```java
// ✅ BEST — one pass, key and value together
for (Map.Entry<K,V> e : map.entrySet())
    System.out.println(e.getKey() + "=" + e.getValue());

// ❌ SLOWER — keySet + get() does a second lookup for every key
for (K k : map.keySet()) System.out.println(k + "=" + map.get(k));

// Java 8
map.forEach((k, v) -> ...);
```

---

## ❓ Q195. How would you design a good `hashCode()` for a key class?

Use all fields that participate in `equals`, combine with the 31-multiplier pattern (or just `Objects.hash`):

```java
@Override public int hashCode() { return Objects.hash(name, age); }
```

> [!note] `Objects.hash(...)` creates a varargs array — in ultra-hot code, write the manual `31 * result + field` version to avoid allocation.

---

## ❓ Q196. How do you sort a `HashMap` by value?

```java
LinkedHashMap<String,Integer> sorted = map.entrySet().stream()
    .sorted(Map.Entry.comparingByValue(Comparator.reverseOrder()))
    .collect(Collectors.toMap(
        Map.Entry::getKey, Map.Entry::getValue,
        (a, b) -> a, LinkedHashMap::new));   // LinkedHashMap keeps the order!
```

---

# 🔑 Section 4 — Other Map Implementations (Q197–Q208)

## ❓ Q197. `HashMap` vs `LinkedHashMap` vs `TreeMap`? ⭐⭐

| | `HashMap` | `LinkedHashMap` | `TreeMap` |
|---|-----------|-----------------|-----------|
| Order | ❌ none | ✅ insertion (or access) | ✅ **sorted by key** |
| Internal | array + list/tree | HashMap + doubly linked list | **Red-Black Tree** |
| get/put | O(1) | O(1) | **O(log n)** |
| Null key | ✅ 1 | ✅ 1 | ❌ |
| Extra memory | low | +2 pointers per entry | tree nodes |
| Implements | `Map` | `Map` | `NavigableMap`, `SortedMap` |

---

## ❓ Q198. How do you build an LRU cache with `LinkedHashMap`? ⭐

```java
class LRUCache<K,V> extends LinkedHashMap<K,V> {
    private final int capacity;
    LRUCache(int capacity) {
        super(16, 0.75f, true);          // ⭐ true = ACCESS order, not insertion
        this.capacity = capacity;
    }
    @Override protected boolean removeEldestEntry(Map.Entry<K,V> eldest) {
        return size() > capacity;        // auto-evict the least recently used
    }
}
```
This is a classic interview coding question — knowing the 3-argument constructor is the trick. 🎩

---

## ❓ Q199. What extra methods does `TreeMap` give you?

```java
map.firstKey();  map.lastKey();
map.headMap(k);  map.tailMap(k);  map.subMap(a, b);
map.floorKey(k);      // greatest key ≤ k
map.ceilingKey(k);    // smallest key ≥ k
map.lowerKey(k);      // strictly <
map.higherKey(k);     // strictly >
map.descendingMap();
map.pollFirstEntry();
```
Very useful for range queries, "find the nearest value", scheduling, and leaderboard problems. 🎯

---

## ❓ Q200. How does `TreeMap` sort? What if the key is not `Comparable`?

By **natural order** (`compareTo`) or by a `Comparator` passed to the constructor. If neither exists → `ClassCastException` at runtime on the **first put** that needs comparison.

```java
TreeMap<Person,String> m = new TreeMap<>(Comparator.comparing(Person::getName));
```

---

## ❓ Q201. What is `WeakHashMap`?

Keys are held by **weak references** — if no other strong reference points to a key, the GC removes that entry automatically.

**Use:** caches and metadata that must not prevent objects from being collected.

---

## ❓ Q202. What is `IdentityHashMap`?

Uses `==` instead of `equals()` for key comparison. Used in serialization frameworks and graph traversal to track "have I seen this exact object?"

---

## ❓ Q203. What is `EnumMap` and why is it fast?

A `Map` whose keys are enum constants. Internally it is just an **array indexed by `ordinal()`** — no hashing, no collisions, extremely compact and fast. ⚡ Always prefer it over `HashMap<SomeEnum, V>`.

---

## ❓ Q204. What is `Properties`?

`Hashtable<Object,Object>` subclass for configuration strings, with `load()`/`store()` for `.properties` files. Legacy but still common.

---

## ❓ Q205. What is `Map.Entry`? Can you modify it?

An interface representing one key→value pair. `entry.setValue(v)` writes through to the map ✅, but `setKey` does not exist (that would break the bucket placement).

Java 9 added immutable `Map.entry(k, v)`.

---

## ❓ Q206. How do you create immutable maps?

```java
Map<String,Integer> m1 = Map.of("a", 1, "b", 2);            // up to 10 pairs
Map<String,Integer> m2 = Map.ofEntries(Map.entry("a", 1));  // any number
Map<String,Integer> m3 = Collections.unmodifiableMap(other);// ⚠️ a VIEW, not a copy
Map<String,Integer> m4 = Map.copyOf(other);                 // true immutable copy
```

> [!warning] `unmodifiableMap` is only a **view** — if someone still holds the original map, they can change it and your "immutable" view changes too.

---

## ❓ Q207. `ConcurrentHashMap` vs `Collections.synchronizedMap()`?

| | `ConcurrentHashMap` | `synchronizedMap` |
|---|---------------------|-------------------|
| Lock | fine-grained (per bucket) | one lock for the whole map |
| Concurrent reads | ✅ lock-free | ❌ blocked |
| Iteration | weakly consistent, safe | must be manually synchronized |
| Performance under load | ⚡ much better | 🐢 |

---

## ❓ Q208. Is `ConcurrentHashMap` fully atomic?

Individual operations are atomic, but **compound** ones are not unless you use the atomic APIs:

```java
// ❌ race condition
if (!map.containsKey(k)) map.put(k, v);

// ✅ atomic
map.putIfAbsent(k, v);
map.computeIfAbsent(k, key -> expensive(key));
```

---

# 🎯 Section 5 — Set Family (Q209–Q216)

## ❓ Q209. `HashSet` vs `LinkedHashSet` vs `TreeSet`? ⭐

| | `HashSet` | `LinkedHashSet` | `TreeSet` |
|---|-----------|-----------------|-----------|
| Backed by | `HashMap` | `LinkedHashMap` | `TreeMap` |
| Order | none | insertion | sorted |
| add/contains | O(1) | O(1) | O(log n) |
| Null | ✅ 1 | ✅ 1 | ❌ |

---

## ❓ Q210. How does `HashSet` work internally? ⭐

It **is** a `HashMap` in disguise. Each element becomes a **key**, and all values point to one shared dummy object:

```java
private static final Object PRESENT = new Object();
public boolean add(E e) { return map.put(e, PRESENT) == null; }
```
That is why `HashSet` gives O(1) `contains()` and why elements need correct `equals`/`hashCode`.

---

## ❓ Q211. How does `HashSet` detect duplicates?

Same rule as `HashMap` keys: same bucket (hash) **and** `equals()` returns true → duplicate → `add` returns `false` and nothing is stored.

---

## ❓ Q212. What happens if you add an object twice with a bad `equals`?

Both copies are stored — your Set now contains logical duplicates. 🐞 This is the practical consequence of skipping `equals`/`hashCode`.

---

## ❓ Q213. What extra methods does `TreeSet` provide?

`first()`, `last()`, `floor()`, `ceiling()`, `higher()`, `lower()`, `headSet()`, `tailSet()`, `subSet()`, `descendingSet()`, `pollFirst()`, `pollLast()`.

---

## ❓ Q214. What is `EnumSet`?

A high-performance `Set` for enum constants, implemented as a **bit vector** (a single `long` for ≤64 constants). Operations are pure bitwise math — dramatically faster and smaller than `HashSet`. ⚡

```java
EnumSet<Day> weekend = EnumSet.of(Day.SAT, Day.SUN);
EnumSet<Day> weekdays = EnumSet.complementOf(weekend);
EnumSet<Day> all = EnumSet.allOf(Day.class);
```

---

## ❓ Q215. How do you perform set operations (union, intersection, difference)?

```java
Set<Integer> a = new HashSet<>(List.of(1,2,3));
Set<Integer> b = new HashSet<>(List.of(2,3,4));

Set<Integer> union = new HashSet<>(a); union.addAll(b);        // [1,2,3,4]
Set<Integer> inter = new HashSet<>(a); inter.retainAll(b);     // [2,3]
Set<Integer> diff  = new HashSet<>(a); diff.removeAll(b);      // [1]
```

---

## ❓ Q216. Why is there no `ConcurrentHashSet`?

Because you can build one:
```java
Set<String> set = ConcurrentHashMap.newKeySet();          // ✅ Java 8
Set<String> set2 = Collections.newSetFromMap(new ConcurrentHashMap<>());
```
Also `CopyOnWriteArraySet` exists for read-heavy cases.

---

# 🚦 Section 6 — Queue, Deque & PriorityQueue (Q217–Q224)

## ❓ Q217. What is a `Queue`? What are its two method families? ⭐

FIFO — first in, first out.

| Action | Throws exception | Returns special value |
|--------|------------------|-----------------------|
| Insert | `add(e)` | `offer(e)` → false |
| Remove | `remove()` | `poll()` → null |
| Examine | `element()` | `peek()` → null |

> [!tip] In bounded queues, always prefer `offer`/`poll`/`peek` — exceptions for a full queue are not an error condition.

---

## ❓ Q218. What is a `Deque`?

**D**ouble **E**nded **Que**ue — insert and remove from **both ends**. Can act as both a **queue** (FIFO) and a **stack** (LIFO).

```java
Deque<Integer> d = new ArrayDeque<>();
d.addFirst(1); d.addLast(2);
d.pollFirst(); d.pollLast();
d.push(1); d.pop();   // stack style (operates on the head)
```

---

## ❓ Q219. `ArrayDeque` vs `LinkedList` as a Deque?

`ArrayDeque` uses a **circular array** → better cache locality, less memory, faster in almost all cases. `LinkedList` only wins if you need `List` index operations too.

> [!warning] `ArrayDeque` does **not** allow `null` — because `null` is the "empty" signal for `poll()`/`peek()`.

---

## ❓ Q220. What is a `PriorityQueue`? ⭐

A queue where `poll()` always returns the **smallest** element (by natural order or a `Comparator`), backed by a **binary min-heap** stored in an array.

```java
PriorityQueue<Integer> minHeap = new PriorityQueue<>();
PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Comparator.reverseOrder());
PriorityQueue<Task> byPriority = new PriorityQueue<>(Comparator.comparingInt(Task::getP));
```

| Operation | Time |
|---|---|
| `offer` / `poll` | O(log n) |
| `peek` | O(1) |
| `contains` / `remove(Object)` | O(n) |

> [!danger] Biggest trap
> **Iterating a `PriorityQueue` does NOT give sorted order!** Only `poll()` does. The array is a heap, not a sorted list. Printing it directly shows heap order.

---

## ❓ Q221. What is `BlockingQueue`?

A queue that **blocks** the thread when it is empty (on take) or full (on put) — the backbone of the producer-consumer pattern.

| | Behaviour |
|---|---|
| `put(e)` | blocks until space is free |
| `take()` | blocks until an element exists |
| `offer(e, timeout, unit)` | waits up to a timeout |

Implementations: `ArrayBlockingQueue` (bounded), `LinkedBlockingQueue`, `PriorityBlockingQueue`, `SynchronousQueue`, `DelayQueue`. Details in [[01 - Java/Interview/05 - Concurrency|Part 5 — Concurrency]].

---

## ❓ Q222. How do you implement a stack and a queue in modern Java?

```java
Deque<Integer> stack = new ArrayDeque<>();   // push / pop / peek — LIFO
Queue<Integer> queue = new ArrayDeque<>();   // offer / poll / peek — FIFO
```
Skip `java.util.Stack` (legacy, synchronized, extends `Vector`).

---

## ❓ Q223. Real use cases for `PriorityQueue`?

Task schedulers, Dijkstra's shortest path, A* search, "top K elements" problems, merging K sorted lists, event simulation. 🧠

---

## ❓ Q224. How do you find the top K largest elements efficiently?

Keep a **min-heap of size K** — O(n log k) time, O(k) memory:
```java
PriorityQueue<Integer> heap = new PriorityQueue<>();   // min-heap
for (int n : nums) {
    heap.offer(n);
    if (heap.size() > k) heap.poll();   // drop the smallest
}
```

---

# 🔄 Section 7 — Iterator, Fail-Fast & CME (Q225–Q232)

## ❓ Q225. What is `ConcurrentModificationException`? ⭐⭐

Thrown when a collection is **structurally modified** while being iterated (outside the iterator's own `remove()`).

**It is NOT only about threads** — a single-threaded for-each loop with `list.remove()` throws it too.

---

## ❓ Q226. How does the fail-fast mechanism work internally? ⭐

Each collection has an internal counter `modCount` that increments on every structural change. When the iterator is created, it copies it into `expectedModCount`. On every `next()`:

```java
final void checkForComodification() {
    if (modCount != expectedModCount) throw new ConcurrentModificationException();
}
```

> [!note] It is a **best-effort bug detector**, not a guarantee. The JDK explicitly says you must not rely on it for program correctness.

---

## ❓ Q227. Fail-fast vs Fail-safe? ⭐

| | **Fail-fast** | **Fail-safe (weakly consistent)** |
|---|---------------|-----------------------------------|
| On modification | throws CME | continues silently |
| Works on | the actual collection | a snapshot / a tolerant view |
| Memory | low | may copy (`CopyOnWrite`) |
| Sees new changes? | n/a | may or may not |
| Examples | `ArrayList`, `HashMap`, `HashSet` | `ConcurrentHashMap`, `CopyOnWriteArrayList` |

---

## ❓ Q228. `Iterator` vs `ListIterator`?

| | `Iterator` | `ListIterator` |
|---|-----------|----------------|
| Direction | forward only | **both directions** |
| Available on | any `Collection` | `List` only |
| Can add? | ❌ | ✅ `add()` |
| Can replace? | ❌ | ✅ `set()` |
| Index access | ❌ | `nextIndex()`, `previousIndex()` |

---

## ❓ Q229. `Iterator` vs `Enumeration`?

`Enumeration` is the legacy version (`hasMoreElements`, `nextElement`), has **no `remove()`**, and is not fail-fast. Only in `Vector`, `Hashtable`, `StringTokenizer`.

---

## ❓ Q230. Can you modify a collection during a for-each loop at all?

You can change an **element's internal state** (non-structural). You cannot **add or remove** elements. Also `list.set(i, v)` is allowed since it does not change `modCount`.

---

## ❓ Q231. Why does removing the second-to-last element sometimes NOT throw CME? 😈

A famous quirk: `hasNext()` is implemented as `cursor != size`. After removing the second-to-last element, `cursor` accidentally equals the new `size`, so the loop **exits early without checking** `modCount` — silently skipping an element instead of throwing.

```java
List<String> list = new ArrayList<>(List.of("a","b","c"));
for (String s : list) if (s.equals("b")) list.remove(s);   // no exception, but wrong result!
```
This is exactly why you must never rely on fail-fast for correctness. ⚠️

---

## ❓ Q232. What is a "weakly consistent" iterator?

It reflects the state of the collection at some point at or since creation, never throws CME, and **may or may not** show later modifications. Used by all `java.util.concurrent` collections.

---

# 🛠️ Section 8 — Collections Utility & Immutable Collections (Q233–Q240)

## ❓ Q233. Most useful `Collections` methods

```java
Collections.sort(list);  Collections.sort(list, cmp);
Collections.reverse(list);
Collections.shuffle(list);
Collections.max(list);  Collections.min(list);
Collections.frequency(list, x);
Collections.binarySearch(list, key);      // list must be sorted
Collections.swap(list, i, j);
Collections.fill(list, value);
Collections.nCopies(3, "x");
Collections.disjoint(a, b);               // true if no common element
Collections.emptyList();  Collections.singletonList(x);
Collections.unmodifiableList(list);
Collections.synchronizedList(list);
Collections.addAll(list, "a", "b");
```

---

## ❓ Q234. `Collections.emptyList()` vs `new ArrayList<>()`?

`emptyList()` returns a **shared immutable singleton** — zero allocation. Use it for return values when there is nothing to return (never return `null` from a method that returns a collection ✅).

---

## ❓ Q235. `unmodifiableList()` vs `List.copyOf()` vs `List.of()`?

| | Immutable? | Copies data? |
|---|---|---|
| `Collections.unmodifiableList(x)` | ⚠️ **view** — original can still change | ❌ |
| `List.copyOf(x)` | ✅ truly | ✅ |
| `List.of(a, b)` | ✅ truly | n/a |

---

## ❓ Q236. Are immutable collections deeply immutable?

**No.** The list cannot be structurally changed, but the **objects inside** can still be mutated if they are mutable. Immutability is only one level deep. 🧅

---

## ❓ Q237. How does `Collections.binarySearch()` behave when the element is missing?

Returns `-(insertionPoint) - 1` — a negative number telling you where it *would* go:
```java
int idx = Collections.binarySearch(list, key);
if (idx < 0) list.add(-idx - 1, key);   // insert keeping order ✅
```

---

## ❓ Q238. What is `Collections.synchronizedList` really doing?

It wraps every method with `synchronized (mutex) { ... }` on a single lock object. Compound operations and iteration still need **your own** synchronized block.

---

## ❓ Q239. How do you remove duplicates from a List, preserving order?

```java
List<String> unique = new ArrayList<>(new LinkedHashSet<>(list));      // ✅ order kept
List<String> unique2 = list.stream().distinct().toList();              // Java 16
```

---

## ❓ Q240. How do you choose the right collection in an interview design question? ⭐

Ask yourself in this order:
1. **Key→value?** → `Map`. Sorted keys? `TreeMap`. Insertion order? `LinkedHashMap`. Concurrent? `ConcurrentHashMap`. Enum key? `EnumMap`.
2. **Unique elements?** → `Set` (same sub-questions).
3. **Ordered with duplicates + index access?** → `ArrayList`.
4. **Both ends / stack / queue?** → `ArrayDeque`.
5. **Always need the min/max first?** → `PriorityQueue`.
6. **Producer-consumer across threads?** → `BlockingQueue`.

> [!tip] Saying this decision tree out loud is more impressive than reciting definitions.

---

# ⚡ Section 9 — Big-O Performance Cheat Sheet

| Collection | get/contains | add | remove | Ordered? | Null? | Thread-safe |
|---|---|---|---|---|---|---|
| `ArrayList` | **O(1)** idx / O(n) search | O(1)* | O(n) | insertion | ✅ | ❌ |
| `LinkedList` | O(n) | O(1) ends | O(1) via iterator | insertion | ✅ | ❌ |
| `CopyOnWriteArrayList` | O(1) | O(n) | O(n) | insertion | ✅ | ✅ |
| `HashSet` | O(1) | O(1) | O(1) | ❌ | ✅ 1 | ❌ |
| `LinkedHashSet` | O(1) | O(1) | O(1) | insertion | ✅ 1 | ❌ |
| `TreeSet` | O(log n) | O(log n) | O(log n) | sorted | ❌ | ❌ |
| `HashMap` | O(1) | O(1) | O(1) | ❌ | ✅ | ❌ |
| `LinkedHashMap` | O(1) | O(1) | O(1) | insert/access | ✅ | ❌ |
| `TreeMap` | O(log n) | O(log n) | O(log n) | sorted | ❌ key | ❌ |
| `ConcurrentHashMap` | O(1) | O(1) | O(1) | ❌ | ❌ | ✅ |
| `ArrayDeque` | O(n) | O(1) ends | O(1) ends | insertion | ❌ | ❌ |
| `PriorityQueue` | O(n) | O(log n) | O(log n) poll | heap | ❌ | ❌ |

`*` amortized

---

# 🧩 Section 10 — Quick Fire Round

> [!question]- Is `Map` part of the Collection interface?
> No. `Map` is a separate hierarchy.

> [!question]- Which is faster for `contains()`: `ArrayList` or `HashSet`?
> `HashSet` — O(1) vs O(n). Converting a list to a set before many lookups is a classic optimization.

> [!question]- What happens if you put the same key twice in a HashMap?
> The **value is replaced**, size stays the same, and `put()` returns the old value.

> [!question]- Why is `String` the most common HashMap key?
> Immutable, `hashCode` is cached, and `equals`/`hashCode` are correctly implemented.

> [!question]- Can we store primitives in collections?
> No — only objects. Autoboxing hides this, but `List<int>` does not compile.

> [!question]- Difference between `poll()` and `remove()` on an empty queue?
> `poll()` returns `null`, `remove()` throws `NoSuchElementException`.

> [!question]- Difference between `peek()` and `element()`?
> Same rule: `peek()` returns `null`, `element()` throws.

> [!question]- What is the difference between `Set.add()` returning true/false?
> `true` = added, `false` = duplicate already present.

> [!question]- Does `HashSet` preserve insertion order?
> No. If output looks ordered for small integers, that is a coincidence of hashing, not a guarantee.

> [!question]- What is the default size of a `HashMap` and when does it resize?
> 16 buckets; resizes at 12 entries (16 × 0.75).

> [!question]- Can two threads safely read a `HashMap` with no writes?
> Yes — a read-only `HashMap` is safe, provided it is safely published (e.g. `final` field or made immutable before sharing).

> [!question]- What is `Collections.unmodifiableList` NOT protecting against?
> Changes to the underlying original list, and mutation of the contained objects.

> [!question]- Which collection would you use for a browser back button?
> A `Deque` used as a stack (`ArrayDeque`).

> [!question]- Which collection for an autocomplete prefix search?
> `TreeMap` with `subMap(prefix, prefix + '\uffff')`, or a Trie for large scale.

---

## 🎓 Self-Test Checklist for Part 3

- [ ] I can draw the collections hierarchy and say why `Map` is separate
- [ ] I can explain `HashMap.put()` step by step including hash spreading and `(n-1) & hash`
- [ ] I know the treeify (8) / untreeify (6) / min-table (64) numbers and why
- [ ] I can explain the Java 7 infinite loop bug and the Java 8 fix
- [ ] I can explain the CME `modCount` mechanism and 3 safe ways to remove
- [ ] I can write an LRU cache with `LinkedHashMap` from memory
- [ ] I know the null rules for every major collection
- [ ] I can recite the Big-O table for the top 6 collections
- [ ] I can walk through the "which collection should I use" decision tree

---

> [!success] ✅ Part 3 complete — 86 questions (Q155–Q240)
> **Next up ➜ Part 4: ⚠️ Exceptions & Generics** — the `Throwable` hierarchy, checked vs unchecked, try-with-resources, custom exceptions, `finally` traps, exception chaining, plus generics: type erasure, bounded types, wildcards, **PECS**, and why you cannot create a generic array.
>
> 👉 Type: **"give me part 4"**

#java #interview #core-java #collections #part3
