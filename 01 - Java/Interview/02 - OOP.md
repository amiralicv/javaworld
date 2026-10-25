---
type: interview
series: Java Interview
part: 2
tags: [java, interview]
---

# 🧬 Java Core Interview Reference — Part 2: OOP Deep Dive

> [!info] About this note
> **Part 2 of 9** — Object Oriented Programming
> Format: Question ➜ Short answer ➜ Deep answer ➜ Code ➜ Interview trap
> Previous: [[01 - Java/Interview/01 - Basics|Part 1 — Basics]]
> Tags: #java #interview #core-java #oop

---

## 🗺️ Series Map

| Part | Topic | Status |
|------|-------|--------|
| 1 | ☕ Language Basics & Fundamentals | ✅ |
| **2** | 🧬 OOP Deep Dive | ✅ You are here |
| 3 | 📦 Collections Framework | ⏳ |
| 4 | ⚠️ Exceptions & Generics | ⏳ |
| 5 | 🧵 Multithreading & Concurrency | ⏳ |
| 6 | 🧠 JVM Memory, GC & Class Loading | ⏳ |
| 7 | 🚀 Java 8+ (Lambda, Stream, Optional) | ⏳ |
| 8 | 💾 I/O, Serialization, Reflection, Annotations | ⏳ |
| 9 | 🎯 Design Patterns + Tricky Output Puzzles | ⏳ |

---

## 📑 Table of Contents

- [[#🏛️ Section 1 — The Four Pillars (Q71–Q78)]]
- [[#🧬 Section 2 — Inheritance (Q79–Q90)]]
- [[#🎭 Section 3 — Polymorphism, Overloading & Overriding (Q91–Q104)]]
- [[#🎨 Section 4 — Abstract Class vs Interface (Q105–Q116)]]
- [[#🧱 Section 5 — The Object Class & equals/hashCode (Q117–Q126)]]
- [[#🔒 Section 6 — Encapsulation & Immutable Classes (Q127–Q132)]]
- [[#🪆 Section 7 — Inner & Nested Classes (Q133–Q138)]]
- [[#⚖️ Section 8 — Comparable vs Comparator (Q139–Q142)]]
- [[#👯 Section 9 — Cloning & Object Copy (Q143–Q146)]]
- [[#🏷️ Section 10 — Enum, Record, Sealed Class (Q147–Q154)]]
- [[#🧩 Section 11 — Quick Fire Round]]

---

# 🏛️ Section 1 — The Four Pillars (Q71–Q78)

## ❓ Q71. What are the four pillars of OOP? ⭐⭐

| Pillar | One line | Java tool |
|--------|----------|-----------|
| 🔒 **Encapsulation** | Hide data, expose behaviour | `private` fields + getters/setters |
| 🎨 **Abstraction** | Show *what*, hide *how* | `abstract class`, `interface` |
| 🧬 **Inheritance** | Reuse and specialize | `extends`, `implements` |
| 🎭 **Polymorphism** | One interface, many forms | overriding + overloading |

> [!tip] How to answer well
> Do not recite definitions. Give **one real example each**:
> "Encapsulation = my `BankAccount` keeps `balance` private so nobody can set it to −500 directly; `withdraw()` validates first."

---

## ❓ Q72. Encapsulation vs Abstraction — what is the real difference? ⭐

They are often confused. The clean separation:

| | Encapsulation | Abstraction |
|---|---------------|-------------|
| Question it answers | **How do I protect data?** | **What should the user see?** |
| Level | implementation level | design level |
| Achieved by | access modifiers | abstract classes / interfaces |
| Focus | data hiding | complexity hiding |

**Analogy 🚗:** Abstraction = you press the brake pedal and the car stops (you don't need to know about hydraulics). Encapsulation = the brake fluid is sealed inside the system so you cannot touch it.

---

## ❓ Q73. What is a class and what is an object?

- **Class** = blueprint / template. No memory for instance data until instantiated.
- **Object** = an instance of a class. Lives on the **heap**, has state (fields) + behaviour (methods) + identity (address).

```java
class Car { String model; void drive() {} }   // blueprint
Car c = new Car();                            // object on heap, `c` is a reference on stack
```

---

## ❓ Q74. What exactly happens when you write `new Car()`?

1. JVM checks whether class `Car` is loaded → if not, **load, link, initialize** (statics run once)
2. Allocate memory on the **heap** for instance fields
3. Set all fields to **default values** (0 / null / false)
4. Run **instance initializer blocks** and field initializers, top to bottom
5. Run the **constructor** body (after `super()` finishes first)
6. Return the **reference** to the variable

---

## ❓ Q75. What is composition? Composition vs Inheritance? ⭐⭐

- **Inheritance** = "IS-A" → `Dog extends Animal`
- **Composition** = "HAS-A" → `Car has an Engine`

```java
class Engine { void start() {} }

class Car {
    private final Engine engine = new Engine();  // composition
    void start() { engine.start(); }
}
```

**Why composition is usually better:**

| Inheritance ⚠️ | Composition ✅ |
|---|---|
| Tight coupling to parent | Loose coupling |
| Fixed at compile time | Can swap at runtime |
| Breaks encapsulation (subclass sees parent internals) | Parent internals stay hidden |
| Only one parent class | Combine many components |
| Parent change breaks children (fragile base class) | Isolated |

> [!tip] Golden sentence
> **"Favour composition over inheritance."** — *Effective Java*, Item 18. Use inheritance only when there is a **true IS-A** relationship **and** the parent was designed for extension (documented + non-final).

---

## ❓ Q76. Give an example where inheritance is the WRONG choice.

Classic: `class Stack extends ArrayList`.
Now someone can call `stack.add(0, x)` and insert into the middle — the LIFO guarantee is destroyed. `Stack` is **not** an `ArrayList`; it **uses** one.

Real JDK mistake: `java.util.Stack extends Vector` and `Properties extends Hashtable` — both are considered design errors today.

---

## ❓ Q77. What is coupling and cohesion?

- **Coupling** = how much one class depends on another → we want **low** 🔽
- **Cohesion** = how focused one class is on a single job → we want **high** 🔼

A class named `UserManagerHelperUtils` that sends emails, saves to DB and formats PDFs has **low cohesion**. Split it.

---

## ❓ Q78. What are the SOLID principles? (short version)

| Letter | Name | Meaning |
|--------|------|---------|
| **S** | Single Responsibility | One class, one reason to change |
| **O** | Open/Closed | Open for extension, closed for modification |
| **L** | Liskov Substitution | A subclass must work anywhere the parent works |
| **I** | Interface Segregation | Many small interfaces > one fat interface |
| **D** | Dependency Inversion | Depend on abstractions, not concrete classes |

**Liskov violation example:** `Square extends Rectangle` — setting width on a Square also changes height, so code written for `Rectangle` breaks. 🟥

---

# 🧬 Section 2 — Inheritance (Q79–Q90)

## ❓ Q79. What is inheritance and what are its types in Java?

| Type | Supported? | Note |
|------|:---------:|------|
| Single (`B extends A`) | ✅ | |
| Multilevel (`C extends B extends A`) | ✅ | |
| Hierarchical (`B`, `C` both extend `A`) | ✅ | |
| **Multiple** (`C extends A, B`) | ❌ classes | ✅ via **interfaces** |
| Hybrid | ❌ classes | ✅ via interfaces |

---

## ❓ Q80. Why does Java NOT support multiple inheritance of classes? ⭐⭐

**The Diamond Problem** 💎

```
      A          class A { void show(){} }
     / \
    B   C        B and C both override show()
     \ /
      D          D extends B, C → which show() runs? ❌ ambiguous
```

Also: constructor chaining and state duplication become ambiguous. Java's designers chose simplicity.

**Interfaces solve it** because (before Java 8) they had no implementation and no state — nothing to conflict.

---

## ❓ Q81. But Java 8 added default methods — is the diamond problem back?

**Yes, partially — and Java forces you to resolve it manually.**

```java
interface A { default void show() { System.out.println("A"); } }
interface B { default void show() { System.out.println("B"); } }

class C implements A, B {
    @Override
    public void show() {
        A.super.show();   // ✅ you MUST choose explicitly
    }
}
```
Without the override → **compile error**. Java refuses to guess. ✅

**Resolution rules when conflicts happen:**
1. **Class wins** over interface (concrete method beats default method)
2. **More specific sub-interface** wins over super-interface
3. Otherwise → you must override explicitly

---

## ❓ Q82. What is inherited and what is NOT inherited?

| Inherited ✅ | Not inherited ❌ |
|---|---|
| public / protected members | `private` members |
| default members (same package only) | constructors |
| static members (accessible, but hidden not overridden) | initializer blocks |

> [!warning] Trap: a `private` field is **not accessible**, but it **does exist in memory** inside the child object. The child just cannot see it directly — only via parent's public methods.

---

## ❓ Q83. Can a subclass access a private member of the parent?

**No**, not directly. Only through inherited `public`/`protected` methods (getters).

---

## ❓ Q84. What is the parent of every class?

`java.lang.Object`. If you write `class A {}`, the compiler makes it `class A extends Object`.

---

## ❓ Q85. Does the constructor get inherited?

**No.** But the child constructor **must** call a parent constructor — implicitly `super()` is inserted as the first line if you do not write one.

```java
class Parent { Parent(int x) { } }        // no no-arg constructor
class Child extends Parent {
    Child() { }   // ❌ compile error: implicit super() not found
    // fix: Child() { super(10); }
}
```

---

## ❓ Q86. What is the `super()` call rule?

- Must be the **first statement** in the constructor
- Cannot use `this()` and `super()` together
- If absent, the compiler inserts `super()` automatically
- Cannot be used inside a `static` context

---

## ❓ Q87. What is the fragile base class problem?

If a parent class changes its internal implementation, subclasses that depended on that behaviour break — even though the public API did not change.

**Famous example:** overriding `addAll()` in a subclass of `HashSet` to count elements → breaks because `HashSet.addAll()` internally calls `add()`, so counting happens twice. Self-use is an invisible contract.

---

## ❓ Q88. How do you prevent inheritance?

1. Make the class `final` → `public final class String`
2. Make all constructors `private` (then only static factories create it)
3. Java 17: use `sealed` to allow only specific subclasses

---

## ❓ Q89. What is `protected` really for?

It exists **only** for inheritance: a subclass in a **different package** can access it. Same-package classes get access too (like default).

> [!warning] `protected` members are part of your **public API** for extenders — once released, you can never change them safely.

---

## ❓ Q90. Can we inherit a class with a private constructor?

**No** (from outside). The child cannot call `super()`. That is exactly how `Math` and `Collections` prevent both instantiation and subclassing.

Exception: an **inner class** of the same class can, because private members are visible inside the same top-level class.

---

# 🎭 Section 3 — Polymorphism, Overloading & Overriding (Q91–Q104)

## ❓ Q91. What is polymorphism? Types? ⭐⭐

**Poly = many, morph = form.** One reference, many possible behaviours.

| Type | Also called | When resolved | Java feature |
|------|-------------|---------------|--------------|
| **Compile-time** | static / early binding | compile time | **overloading** |
| **Runtime** | dynamic / late binding | runtime | **overriding** |

```java
Animal a = new Dog();
a.sound();   // "Woof" — decided at RUNTIME by the object, not the reference
```

---

## ❓ Q92. Overloading vs Overriding — the full table ⭐⭐⭐

| | **Overloading** | **Overriding** |
|---|-----------------|----------------|
| Where | same class (or subclass) | parent ↔ child |
| Parameters | **must differ** | **must be identical** |
| Return type | can differ freely | same or **covariant** (subtype) |
| Access modifier | any | cannot be **more restrictive** |
| Exceptions | any | cannot throw **broader checked** exceptions |
| Binding | compile time | runtime |
| `static` methods | ✅ can overload | ❌ hidden, not overridden |
| `private`/`final` | ✅ can overload | ❌ cannot override |

---

## ❓ Q93. Can we overload a method by changing ONLY the return type?

**No.** ❌ The compiler picks methods by the **signature** (name + parameter types). Return type is not part of the signature.

```java
int  get() {}
long get() {}   // ❌ compile error: duplicate method
```

---

## ❓ Q94. Can we overload the `main` method?

**Yes**, but the JVM always starts with `main(String[])`.

```java
public static void main(String[] a) { main(5); }
public static void main(int x) { System.out.println("overloaded " + x); }
```

---

## ❓ Q95. How does the compiler choose which overload to call? ⭐

Order of preference (first match wins):
1. **Exact match**
2. **Widening** (`int → long → float → double`)
3. **Autoboxing** (`int → Integer`)
4. **Varargs** (last resort)

```java
void m(long x)     { System.out.println("long"); }
void m(Integer x)  { System.out.println("Integer"); }
void m(int... x)   { System.out.println("varargs"); }

m(5);   // prints "long" — widening beats boxing beats varargs
```

**Famous trap:**
```java
void m(Object o) { System.out.println("Object"); }
void m(String s) { System.out.println("String"); }
m(null);   // prints "String" — the MOST SPECIFIC type wins
```
If you add `void m(Integer i)` too → `m(null)` becomes **ambiguous** → compile error. ⚠️

---

## ❓ Q96. What are the rules for method overriding? ⭐⭐

✅ Must have:
- same method name
- same parameter list
- same or **covariant** return type
- same or **wider** access modifier
- same or **narrower** checked exceptions

```java
class Parent {
    protected Number get() throws IOException { return 1; }
}
class Child extends Parent {
    @Override
    public Integer get() throws FileNotFoundException { return 2; }
    //  ↑ wider access   ↑ covariant return   ↑ narrower exception  — all ✅
}
```

❌ Cannot override: `static`, `final`, `private` methods, and constructors.

---

## ❓ Q97. Can an overriding method throw a different exception?

- **Unchecked** (RuntimeException, Error) → ✅ any, no restriction
- **Checked** → only the same or a **subclass**; or fewer; or none

```java
class P { void m() throws IOException {} }
class C extends P {
    void m() throws Exception {}   // ❌ Exception is BROADER than IOException
}
```

---

## ❓ Q98. What is covariant return type?

Since Java 5, an overriding method may return a **subtype** of the parent's return type.

```java
class Animal { Animal reproduce() { return new Animal(); } }
class Dog extends Animal {
    @Override Dog reproduce() { return new Dog(); }   // ✅ Dog is-a Animal
}
```
This removes the need for casting by the caller. Widely used in **builder patterns** and `clone()`.

---

## ❓ Q99. What is dynamic method dispatch? How does the JVM do it?

**Answer:** The mechanism that picks the **overridden** method at runtime based on the actual object.

**Under the hood [Likely]:** every class has a **vtable** (virtual method table) in method area. The reference points to the object → the object header points to its class → the class holds the pointer to the correct method implementation. The JIT often optimizes this to a direct call when only one implementation exists (**monomorphic inline caching**).

---

## ❓ Q100. Fields are NOT polymorphic — the variable hiding trap ⭐

```java
class Parent { String name = "Parent"; String get() { return "Parent"; } }
class Child extends Parent { String name = "Child"; String get() { return "Child"; } }

Parent p = new Child();
System.out.println(p.name);    // "Parent"  ← FIELD: resolved by REFERENCE type
System.out.println(p.get());   // "Child"   ← METHOD: resolved by OBJECT type
```

> [!danger] Memorize: **methods are overridden (runtime), fields are hidden (compile time).** Same for `static` methods.

---

## ❓ Q101. What is upcasting and downcasting?

```java
Animal a = new Dog();          // upcasting — implicit, always safe ✅
Dog d = (Dog) a;               // downcasting — explicit, may fail ⚠️
Cat c = (Cat) a;               // 💥 ClassCastException at runtime
```

**Safe way:**
```java
if (a instanceof Dog dog) {    // Java 16 pattern matching — casts automatically
    dog.bark();
}
```

---

## ❓ Q102. What does `instanceof` return for `null`?

**Always `false`** — never throws NPE.
```java
String s = null;
System.out.println(s instanceof String);   // false ✅
```

---

## ❓ Q103. What is the `@Override` annotation? Is it required?

Not required, but **always use it**. It makes the compiler verify that you really are overriding. Without it, a typo like `hashcode()` instead of `hashCode()` silently creates a **new method** and your `HashMap` breaks. 🐞

---

## ❓ Q104. Can you override a method and make it `synchronized` / `final` / `static`?

- `synchronized` → ✅ yes, it is not part of the signature
- `final` → ✅ yes (it just stops further overriding)
- `static` → ❌ an instance method cannot become static and vice versa → compile error

---

# 🎨 Section 4 — Abstract Class vs Interface (Q105–Q116)

## ❓ Q105. What is an abstract class?

A class that **cannot be instantiated** and may contain abstract (unimplemented) methods.

```java
abstract class Shape {
    protected String color;                 // ✅ state allowed
    Shape(String color) { this.color = color; }   // ✅ constructor allowed
    abstract double area();                 // no body
    void describe() { System.out.println(color + " area=" + area()); }  // concrete
}
```

Rules:
- If a class has **any** abstract method → the class must be abstract
- An abstract class **may have zero** abstract methods (still not instantiable)
- Abstract methods cannot be `private`, `static`, or `final`

---

## ❓ Q106. Can an abstract class have a constructor? Why?

**Yes.** It is never called by `new Shape()`, but it **is** called via `super()` when a concrete subclass is created — to initialize the inherited state.

---

## ❓ Q107. Abstract class vs Interface — full comparison ⭐⭐⭐

| | **Abstract Class** | **Interface** |
|---|--------------------|---------------|
| Keyword | `abstract class` | `interface` |
| Inheritance | single (`extends`) | multiple (`implements`) |
| State / fields | ✅ any instance fields | ❌ only `public static final` constants |
| Constructor | ✅ yes | ❌ no |
| Method types | abstract, concrete, static, final, private | abstract, `default`, `static`, `private` (J9) |
| Access modifiers | any | members are implicitly `public` |
| Relationship | **IS-A**, shares code | **CAN-DO**, defines capability |
| Use when | related classes share code + state | unrelated classes share a contract |

**Rule of thumb 🎯:** `Bird`, `Plane`, `Superman` are unrelated but all `implements Flyable`. `Dog` and `Cat` both `extends Animal` because they share fields and code.

---

## ❓ Q108. What can an interface contain in modern Java?

```java
public interface Service {
    int MAX = 10;                                   // public static final (implicit)

    void execute();                                 // public abstract (implicit)

    default void log() {                            // Java 8
        System.out.println("running " + helper());
    }

    static Service create() { return new Impl(); }  // Java 8 — not inherited

    private String helper() { return "x"; }         // Java 9 — code reuse for defaults

    private static String util() { return "y"; }    // Java 9
}
```

---

## ❓ Q109. Why were `default` methods added in Java 8? ⭐

**Backward compatibility.** They wanted to add `stream()` to `Collection`. Adding an abstract method would break **every** existing implementation in the world. A `default` method lets the interface evolve without breaking anyone. 🛠️

---

## ❓ Q110. Can an interface extend another interface? Can it extend a class?

- Interface `extends` interface → ✅ and it can extend **multiple** interfaces
- Interface extends class → ❌ never

```java
interface A {}
interface B {}
interface C extends A, B {}   // ✅ allowed
```

---

## ❓ Q111. Can an abstract class implement an interface without providing the methods?

**Yes** — it can leave them abstract for its subclasses. This is the **Adapter** idea.

```java
abstract class BaseHandler implements Handler { /* implements nothing */ }
```

---

## ❓ Q112. What is a marker interface? Give examples.

An interface with **no members**, used only to tag a class with metadata for the JVM or a framework.

Examples: `Serializable`, `Cloneable`, `RandomAccess`, `Remote`.

```java
if (obj instanceof Serializable) { /* safe to serialize */ }
```

> [!note] Today **annotations** are usually preferred (`@FunctionalInterface`, `@Deprecated`), but marker interfaces still win when you need a **type** for compile-time checks and for `instanceof`.

---

## ❓ Q113. What is a functional interface?

An interface with exactly **one abstract method** (SAM). Can be implemented by a lambda.

```java
@FunctionalInterface
interface Calculator {
    int apply(int a, int b);          // exactly one abstract method
    default Calculator twice() { ... } // defaults do not count ✅
}

Calculator add = (a, b) -> a + b;
```

> [!note] `default`, `static`, and `Object`'s public methods (`equals`, `hashCode`, `toString`) do **not** count toward the one-abstract-method rule. More in [[01 - Java/Interview/07 - Java 8 & Modern Java|Part 7 — Java 8 & Modern Java]].

---

## ❓ Q114. Can we create an object of an interface or abstract class?

Not directly — but you **can** use an **anonymous class**, which creates a hidden subclass:

```java
Runnable r = new Runnable() {          // creates an anonymous class, not a Runnable object
    public void run() { System.out.println("hi"); }
};
```

---

## ❓ Q115. What happens if a class implements two interfaces with the same abstract method?

**Nothing bad** — one implementation satisfies both. Conflict only occurs with two **default** methods (see Q81).

---

## ❓ Q116. When would you choose abstract class over interface in real design?

Choose **abstract class** when:
- you need shared **state** (fields) or a constructor
- you want to provide a **template** (`AbstractList`, `AbstractMap`)
- subclasses are truly the same kind of thing

Choose **interface** when:
- multiple unrelated classes need the capability
- you want to allow multiple inheritance of type
- you are defining a public API contract (better for testing / mocking / DI)

---

# 🧱 Section 5 — The Object Class & equals/hashCode (Q117–Q126)

## ❓ Q117. What methods does `Object` have? ⭐

| Method | Purpose |
|--------|---------|
| `equals(Object)` | logical equality (default: `==`) |
| `hashCode()` | integer hash for hash-based collections |
| `toString()` | text representation (default: `ClassName@hexHash`) |
| `getClass()` | runtime class — `final` |
| `clone()` | shallow copy — `protected` |
| `finalize()` | ⚠️ deprecated / removed |
| `wait()`, `notify()`, `notifyAll()` | thread coordination — `final` |

**Which can be overridden?** `equals`, `hashCode`, `toString`, `clone`, (`finalize`). The rest are `final`.

---

## ❓ Q118. What is the `equals()` contract? ⭐⭐

For non-null references:
1. **Reflexive** — `x.equals(x)` is true
2. **Symmetric** — `x.equals(y)` ⇔ `y.equals(x)`
3. **Transitive** — if `x=y` and `y=z` then `x=z`
4. **Consistent** — repeated calls return the same result
5. **Null** — `x.equals(null)` is always `false`

---

## ❓ Q119. What is the `hashCode()` contract? ⭐⭐

1. If `a.equals(b)` is **true** → `a.hashCode() == b.hashCode()` **must** be true ✅
2. If hash codes are equal → objects **may or may not** be equal (collision allowed)
3. Hash code must stay consistent during one execution while the object does not change

> [!danger] The #1 interview answer
> **"If you override `equals()`, you MUST override `hashCode()`."**
> Otherwise `HashMap`/`HashSet` will "lose" your object: it is stored in bucket A (old hash) and searched in bucket B.

---

## ❓ Q120. Show a correct `equals()` and `hashCode()` implementation.

```java
public class Person {
    private final String name;
    private final int age;

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;                    // 1. fast path
        if (o == null || getClass() != o.getClass())   // 2. type check
            return false;
        Person p = (Person) o;                         // 3. cast
        return age == p.age &&                         // 4. compare fields
               Objects.equals(name, p.name);           //    null-safe
    }

    @Override
    public int hashCode() {
        return Objects.hash(name, age);                // Java 7+
    }
}
```

---

## ❓ Q121. `getClass() != o.getClass()` vs `instanceof` in equals — which is correct?

**Both are used, and they trade off differently:**

| | `getClass()` | `instanceof` |
|---|-------------|--------------|
| Subclass equals parent? | never | possible |
| Symmetry safe? | ✅ always | ⚠️ can break with subclasses |
| Liskov friendly? | ⚠️ strict | ✅ flexible |

*Effective Java* recommendation: use `getClass()` unless you deliberately design a value class where subclasses should be comparable — or better, **prefer composition over inheritance for value classes**.

---

## ❓ Q122. What happens if `hashCode()` always returns the same constant?

The code still **works correctly**, but every object lands in the **same bucket** → `HashMap` degenerates from O(1) to O(n) (or O(log n) after treeification in Java 8). 🐢

---

## ❓ Q123. What happens if you mutate a field used in `hashCode()` after inserting into a HashSet?

The object becomes **unreachable**:

```java
Set<Person> set = new HashSet<>();
Person p = new Person("Ali");
set.add(p);
p.setName("Sara");          // hash changed!
set.contains(p);            // false 😱
set.remove(p);              // fails — memory leak
```

> [!tip] Lesson: **make hash-key classes immutable.**

---

## ❓ Q124. Why override `toString()`?

Default output is `com.app.Person@1b6d3586` — useless in logs. A good `toString()` saves hours of debugging.

```java
@Override public String toString() {
    return "Person{name='" + name + "', age=" + age + "}";
}
```

---

## ❓ Q125. Do two equal objects always have the same reference? Do two objects with the same hash code have to be equal?

- Equal objects → **not necessarily** the same reference (`new String("a").equals("a")` is true, `==` is false)
- Same hash code → **not necessarily** equal (that is a **collision**, perfectly legal)

---

## ❓ Q126. `==` vs `equals()` vs `Objects.equals()` vs `compareTo() == 0`?

```java
a == b                 // reference identity
a.equals(b)            // logical equality, NPE if a is null
Objects.equals(a, b)   // null-safe version ✅
a.compareTo(b) == 0    // ordering equality
```

> [!warning] `BigDecimal` trap: `new BigDecimal("1.0").equals(new BigDecimal("1.00"))` is **false** (scale differs), but `compareTo` returns **0**. For money comparisons use `compareTo`.

---

# 🔒 Section 6 — Encapsulation & Immutable Classes (Q127–Q132)

## ❓ Q127. How do you achieve encapsulation?

1. Make all fields `private`
2. Expose controlled `public` getters/setters
3. Validate inside setters

```java
public class Account {
    private double balance;
    public double getBalance() { return balance; }
    public void deposit(double amount) {
        if (amount <= 0) throw new IllegalArgumentException("must be positive");
        balance += amount;
    }
}
```

> [!tip] Better answer: "Encapsulation is not about writing getters and setters for every field — that is just public fields with extra steps. It is about exposing **behaviour** (`deposit`) instead of **data** (`setBalance`)."

---

## ❓ Q128. How do you create an immutable class? ⭐⭐ (very common)

**The 5 rules:**
1. Make the class `final` (no subclass can break it)
2. Make all fields `private final`
3. No setters — only getters
4. Initialize everything in the constructor
5. **Defensive copy** mutable fields in both the constructor **and** the getters

```java
public final class Employee {
    private final String name;              // String is already immutable ✅
    private final Date joinDate;            // ⚠️ Date is MUTABLE
    private final List<String> skills;

    public Employee(String name, Date joinDate, List<String> skills) {
        this.name = name;
        this.joinDate = new Date(joinDate.getTime());     // defensive copy IN
        this.skills = List.copyOf(skills);                // unmodifiable copy
    }

    public Date getJoinDate() {
        return new Date(joinDate.getTime());              // defensive copy OUT
    }
    public List<String> getSkills() { return skills; }     // already unmodifiable
}
```

---

## ❓ Q129. Why is immutability good?

- 🧵 Thread-safe with zero synchronization
- 🔑 Safe as `Map` keys and `Set` elements
- 🐞 Fewer bugs — no unexpected state change
- 💾 Can be cached and shared freely (String pool, `Integer` cache)

**Cost:** creates more objects. Usually cheap because modern GC handles short-lived objects very well.

---

## ❓ Q130. Is `final class` = immutable class?

**No.** `final` only stops inheritance. A `final` class with a setter is fully mutable.

---

## ❓ Q131. What is a defensive copy and why do we need it?

Without it, the caller keeps a reference to your internal object:

```java
Date d = new Date();
Employee e = new Employee("Ali", d, skills);
d.setTime(0);            // 💥 changes Employee's internal state if no copy was made
```

---

## ❓ Q132. Are getters/setters always necessary?

No. For a pure data carrier, use a **`record`** (Java 16) — it generates the constructor, accessors, `equals`, `hashCode`, and `toString` for you. See Q151.

---

# 🪆 Section 7 — Inner & Nested Classes (Q133–Q138)

## ❓ Q133. What are the four types of nested classes? ⭐

| Type | Declared | Needs outer instance? | Typical use |
|------|----------|:---------------------:|-------------|
| **Static nested** | `static class` inside a class | ❌ | Builder, Node in LinkedList |
| **Inner (non-static)** | `class` inside a class | ✅ | Iterator that needs outer state |
| **Local** | inside a method | ✅ | one method's helper |
| **Anonymous** | on the fly with `new` | depends | listeners, one-off Runnable |

---

## ❓ Q134. Static nested vs Inner class? ⭐

```java
class Outer {
    private int x = 10;
    static class StaticNested { void m() { /* cannot see x directly */ } }
    class Inner { void m() { System.out.println(x); } }  // ✅ sees outer fields
}

Outer.StaticNested s = new Outer.StaticNested();       // no outer object needed
Outer.Inner i = new Outer().new Inner();               // ⚠️ weird but valid syntax
```

> [!warning] Memory leak risk 🩸
> A non-static inner class holds a **hidden reference to the outer instance**. If the inner object lives long (a listener, a static map, a thread), the outer object can never be garbage collected. **Prefer `static` nested classes** unless you truly need the outer state.

---

## ❓ Q135. What is an anonymous class?

A class with no name, declared and instantiated at once. It can extend a class **or** implement an interface — but only one, and it cannot have a constructor.

```java
Comparator<String> byLength = new Comparator<>() {
    public int compare(String a, String b) { return a.length() - b.length(); }
};
```

---

## ❓ Q136. Anonymous class vs Lambda? ⭐

| | Anonymous class | Lambda |
|---|-----------------|--------|
| Target | any interface / abstract class | **functional interface only** |
| `this` refers to | the anonymous object | the **enclosing** object |
| Can hold state | ✅ fields allowed | ❌ |
| Compiled to | separate `Outer$1.class` file | `invokedynamic`, no extra class |
| Readability | verbose | concise |

---

## ❓ Q137. Why must a local variable used inside an inner class be final or effectively final?

Because the inner class **copies** the value (the local variable dies when the method returns, but the object may live longer). If the original could change, the two copies would disagree. Java forbids it to keep them consistent.

```java
void m() {
    int count = 0;
    Runnable r = () -> System.out.println(count);   // ✅ effectively final
    count++;                                        // ❌ now the lambda does not compile
}
```

**Java 8+**: you no longer need to write `final` — "**effectively final**" (never reassigned) is enough.

---

## ❓ Q138. Can an inner class have static members?

- Before Java 16: only `static final` constants
- **Java 16+**: inner classes can declare static members freely ✅

---

# ⚖️ Section 8 — Comparable vs Comparator (Q139–Q142)

## ❓ Q139. `Comparable` vs `Comparator`? ⭐⭐

| | `Comparable` | `Comparator` |
|---|--------------|--------------|
| Package | `java.lang` | `java.util` |
| Method | `compareTo(T o)` | `compare(T a, T b)` |
| Where | **inside** the class | **outside**, separate object |
| How many orders | one (**natural order**) | unlimited |
| Modify original class? | ✅ required | ❌ not needed |
| Used by | `Collections.sort(list)`, `TreeMap` | `Collections.sort(list, cmp)` |

---

## ❓ Q140. Show both in code.

```java
// Natural ordering — inside the class
class Person implements Comparable<Person> {
    String name; int age;
    @Override public int compareTo(Person o) {
        return Integer.compare(this.age, o.age);   // ✅ never use a - b (overflow!)
    }
}

// Custom orderings — outside
Comparator<Person> byName = Comparator.comparing(p -> p.name);
Comparator<Person> byAgeDescThenName =
        Comparator.comparingInt((Person p) -> p.age).reversed()
                  .thenComparing(p -> p.name);

list.sort(byAgeDescThenName);
```

---

## ❓ Q141. What must `compareTo()` return?

- negative → `this` comes **before**
- zero → equal in order
- positive → `this` comes **after**

> [!warning] Never write `return this.age - o.age;` — it **overflows** for large/negative values. Use `Integer.compare(a, b)`.

---

## ❓ Q142. Should `compareTo()` be consistent with `equals()`?

**Strongly recommended.** `TreeSet` and `TreeMap` use `compareTo`, not `equals`. If they disagree, a `TreeSet` will silently drop an element that `equals` says is different.

```java
// BigDecimal is the classic inconsistent example
Set<BigDecimal> hash = new HashSet<>();
hash.add(new BigDecimal("1.0")); hash.add(new BigDecimal("1.00"));  // size 2
Set<BigDecimal> tree = new TreeSet<>();
tree.add(new BigDecimal("1.0")); tree.add(new BigDecimal("1.00"));  // size 1 😱
```

---

# 👯 Section 9 — Cloning & Object Copy (Q143–Q146)

## ❓ Q143. What is `clone()` and the `Cloneable` interface?

`Object.clone()` is `protected` and creates a **field-by-field shallow copy**. To use it, the class must implement the **marker** interface `Cloneable`, otherwise you get `CloneNotSupportedException`.

```java
class Person implements Cloneable {
    @Override public Person clone() throws CloneNotSupportedException {
        return (Person) super.clone();
    }
}
```

---

## ❓ Q144. Shallow copy vs Deep copy? ⭐

```
SHALLOW                          DEEP
original ──┐                     original ──> [ Address A ]
           ├──> [ Address ]
copy ──────┘                     copy ──────> [ Address B ] (new copy)
```

```java
// Deep copy — copy nested mutable objects too
@Override public Person clone() {
    Person p = (Person) super.clone();
    p.address = new Address(this.address);   // manual deep copy
    return p;
}
```

---

## ❓ Q145. Why is `clone()` considered broken?

- `Cloneable` does not declare `clone()` — a broken marker design
- `super.clone()` bypasses the constructor → `final` fields cannot be reassigned
- Checked exception in a place nobody wants it
- Shallow by default → surprising bugs

**Better alternatives:** a **copy constructor**, a **static factory**, a **builder**, or serialization.

```java
public Person(Person other) {                 // copy constructor ✅ clean
    this.name = other.name;
    this.address = new Address(other.address);
}
```

---

## ❓ Q146. How do you deep copy with serialization?

Serialize to bytes and read back — everything in the graph becomes new. Simple but **slow** and requires all classes to be `Serializable`. More in [[01 - Java/Interview/08 - IO & Reflection|Part 8 — IO & Reflection]].

---

# 🏷️ Section 10 — Enum, Record, Sealed Class (Q147–Q154)

## ❓ Q147. What is an `enum`? Can it have fields and methods?

A special class with a fixed set of instances. **Yes**, it can have fields, constructors (implicitly `private`), and methods.

```java
public enum Planet {
    MERCURY(3.30e23, 2.44e6),
    EARTH  (5.98e24, 6.37e6);

    private final double mass, radius;
    Planet(double mass, double radius) { this.mass = mass; this.radius = radius; }
    double surfaceGravity() { return 6.67e-11 * mass / (radius * radius); }
}
```

---

## ❓ Q148. Can an enum extend a class? Implement an interface?

- Extend a class → ❌ (it already extends `java.lang.Enum`)
- Implement an interface → ✅

Each constant can even have its **own body**:
```java
enum Operation {
    PLUS  { int apply(int a, int b) { return a + b; } },
    TIMES { int apply(int a, int b) { return a * b; } };
    abstract int apply(int a, int b);
}
```

---

## ❓ Q149. Useful enum methods

```java
Planet.EARTH.name();        // "EARTH"
Planet.EARTH.ordinal();     // 1 (index — ⚠️ never persist this!)
Planet.valueOf("EARTH");    // enum constant, throws IllegalArgumentException if missing
Planet.values();            // array of all constants
EnumSet.of(Planet.EARTH);   // ⚡ super fast bitset-based Set
EnumMap<Planet, String>     // ⚡ array-based Map
```

---

## ❓ Q150. Why is enum the best Singleton? ⭐

```java
public enum Config {
    INSTANCE;
    public void load() { }
}
```
The JVM guarantees a single instance, it is **thread-safe by construction**, and it is **safe against reflection and serialization attacks** — which the classic `private static final` singleton is not. (*Effective Java*, Item 3)

---

## ❓ Q151. What is a `record`? (Java 16) ⭐

An immutable, transparent data carrier.

```java
public record Point(int x, int y) { }
```
The compiler generates: `private final` fields, a canonical constructor, accessors `x()` / `y()`, `equals`, `hashCode`, `toString`.

**Validation via compact constructor:**
```java
public record Range(int lo, int hi) {
    public Range {                                   // no parameter list
        if (lo > hi) throw new IllegalArgumentException("lo > hi");
    }
}
```

**Restrictions:** implicitly `final`, cannot extend another class, no extra instance fields, but **can** implement interfaces and have static members.

---

## ❓ Q152. Record vs Class vs Lombok `@Data`?

Use a `record` when the type is a **transparent carrier of data** with no hidden state and no mutability. Use a normal class when you need mutability, inheritance, or hidden internal representation. A record is a **language feature**, not code generation at build time like Lombok.

---

## ❓ Q153. What is a `sealed` class/interface? (Java 17) ⭐

Restricts **who** may extend it — controlled inheritance.

```java
public sealed interface Shape permits Circle, Square, Triangle { }

public final class Circle implements Shape { }        // final: closed
public non-sealed class Square implements Shape { }   // reopened for anyone
public sealed class Triangle implements Shape permits Right { }
```

Every permitted subclass must be `final`, `sealed`, or `non-sealed`.

**Why?** It makes the hierarchy **exhaustive**, so `switch` pattern matching does not need a `default`:

```java
double area = switch (shape) {
    case Circle c   -> Math.PI * c.r() * c.r();
    case Square s   -> s.side() * s.side();
    case Triangle t -> 0.5 * t.b() * t.h();
    // no default needed — compiler knows all cases ✅
};
```

---

## ❓ Q154. What is the "algebraic data type" combo everyone mentions in modern Java?

`sealed interface` + `record` + `switch` pattern matching = model your domain exactly and let the compiler check completeness. This is the modern alternative to the classic Visitor pattern. 🎯

---

# 🧩 Section 11 — Quick Fire Round

> [!question]- Can an abstract class be `final`?
> No — direct contradiction.

> [!question]- Can an interface have a `main` method?
> Yes, as a `static` method. It runs fine.

> [!question]- Can we declare a constructor as `abstract`?
> No. Constructors are never inherited, so overriding them is meaningless.

> [!question]- What is the output? `Parent p = new Child(); p.staticMethod();`
> The **Parent's** static method — resolved by reference type (method hiding).

> [!question]- Can a class implement two interfaces that both declare `int getX()` with different return types?
> No — incompatible return types → compile error.

> [!question]- Does overriding `equals` require overriding `hashCode` even if I never use HashMap?
> Yes — you cannot control what future code does with your object. Always keep the contract.

> [!question]- What is a POJO vs a Java Bean?
> POJO = plain object with no framework rules. JavaBean = POJO + no-arg public constructor + private fields + getters/setters + `Serializable`.

> [!question]- Can you override a `private` method?
> No. The child simply defines a **new, unrelated** method — no polymorphism.

> [!question]- What is the diamond problem and how do interfaces avoid it before Java 8?
> Ambiguity from two parents with the same method. Old interfaces had no bodies, so nothing to be ambiguous about.

> [!question]- `IS-A` vs `HAS-A`?
> `IS-A` = inheritance (`Dog extends Animal`). `HAS-A` = composition (`Car has Engine`).

> [!question]- Can you cast `Object o = "hello"` to `Integer`?
> It compiles (both are Objects) but throws `ClassCastException` at runtime.

> [!question]- Is an empty interface useless?
> No — see marker interfaces (`Serializable`).

> [!question]- Can a record be abstract or extend a class?
> No. Records are implicitly `final` and already extend `java.lang.Record`.

---

## 🎓 Self-Test Checklist for Part 2

- [ ] I can explain the diamond problem and how Java 8 default methods resolve it
- [ ] I can recite the overloading vs overriding table
- [ ] I know why fields are hidden but methods are overridden
- [ ] I can write correct `equals`/`hashCode` from memory
- [ ] I can state the 5 rules of an immutable class and explain defensive copy
- [ ] I can explain why inner classes cause memory leaks
- [ ] I know when `Comparable` beats `Comparator` and vice versa
- [ ] I can explain composition over inheritance with the `Stack extends Vector` example
- [ ] I can describe `record`, `sealed`, and pattern-matching `switch`

---

> [!success] ✅ Part 2 complete — 84 questions (Q71–Q154)
> **Next up ➜ Part 3: 📦 Collections Framework** — the hierarchy, `ArrayList` vs `LinkedList`, **HashMap internals** (buckets, load factor, treeification, resize), `ConcurrentModificationException`, fail-fast vs fail-safe, `TreeMap`, `LinkedHashMap` LRU, `Set` family, `Queue`/`Deque`, `Iterator`, and the `Collections` utility class.
>
> 👉 Type: **"give me part 3"**

#java #interview #core-java #oop #part2
