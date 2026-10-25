---
type: interview
series: Java Interview
part: 8
tags: [java, interview]
---

# 💾 Java Core Interview Reference — Part 8: I/O, Serialization, Reflection & Annotations

> [!info] **Part 8 of 9** — File handling, streams, serialization, reflection, annotations, and String internals
> Previous: [[01 - Java/Interview/07 - Java 8 & Modern Java|Part 7 — Java 8 & Modern Java]] | Hub: [[01 - Java/Interview/00 - Overview|Interview Hub]]
> Tags: #java #interview #core-java #io #reflection

---

## 📑 Table of Contents

- [[#📂 Section 1 — I/O Fundamentals (Q557–Q570)]]
- [[#⚡ Section 2 — NIO & Files (Q571–Q580)]]
- [[#📦 Section 3 — Serialization (Q581–Q596)]]
- [[#🔍 Section 4 — Reflection (Q597–Q610)]]
- [[#🏷️ Section 5 — Annotations (Q611–Q620)]]
- [[#🧩 Section 6 — Quick Fire Round]]

---

# 📂 Section 1 — I/O Fundamentals (Q557–Q570)

## ❓ Q557. What is a stream in Java I/O?

A sequence of data flowing from a source to a destination. **Note:** `java.io` streams are completely unrelated to `java.util.stream` (Part 7) — same word, different concept. ⚠️

---

## ❓ Q558. Byte streams vs Character streams? ⭐⭐

| | Byte streams | Character streams |
|---|--------------|-------------------|
| Base classes | `InputStream` / `OutputStream` | `Reader` / `Writer` |
| Unit | 8-bit bytes | 16-bit chars |
| For | images, audio, binary, any file | **text** |
| Encoding aware | ❌ | ✅ handles charset |

**Rule:** text → `Reader`/`Writer`; everything else → `InputStream`/`OutputStream`. 📖

---

## ❓ Q559. Draw the I/O class hierarchy.

```
InputStream                      OutputStream
 ├── FileInputStream              ├── FileOutputStream
 ├── ByteArrayInputStream         ├── ByteArrayOutputStream
 ├── ObjectInputStream            ├── ObjectOutputStream
 └── FilterInputStream            └── FilterOutputStream
      └── BufferedInputStream          ├── BufferedOutputStream
      └── DataInputStream              └── PrintStream

Reader                           Writer
 ├── InputStreamReader            ├── OutputStreamWriter
 │    └── FileReader              │    └── FileWriter
 ├── BufferedReader               ├── BufferedWriter
 └── StringReader                 └── PrintWriter
```

---

## ❓ Q560. What is the Decorator pattern in java.io? ⭐

You wrap streams to add capabilities — this is the textbook example of the Decorator pattern.

```java
new BufferedReader(                 // + buffering
    new InputStreamReader(          // + byte→char conversion with a charset
        new FileInputStream("f.txt"),   // raw bytes
        StandardCharsets.UTF_8));
```

---

## ❓ Q561. Why use buffering? ⭐

Without it, every `read()` is a **system call** — reading a 1 MB file byte by byte means a million syscalls. A buffer reads a large block at once into memory.

The speed difference is typically **10–100×**. Always wrap file streams in a Buffered variant (or use NIO). ⚡

---

## ❓ Q562. `FileReader` vs `InputStreamReader` — which should you use?

`FileReader` uses the **platform default charset** (before Java 18), which makes your program behave differently on different machines — a real production bug source.

```java
// ❌ risky
new FileReader("f.txt");
// ✅ explicit
new InputStreamReader(new FileInputStream("f.txt"), StandardCharsets.UTF_8);
// ✅ modern
Files.newBufferedReader(path, StandardCharsets.UTF_8);
```
Java 18 made UTF-8 the default charset (JEP 400), but being explicit is still correct.

---

## ❓ Q563. How do you read a file — the modern ways? ⭐

```java
// Whole file (small files only)
String content = Files.readString(path);                    // Java 11 ✅
List<String> lines = Files.readAllLines(path);
byte[] bytes = Files.readAllBytes(path);

// Line by line, streaming (large files) ✅
try (Stream<String> lines = Files.lines(path)) {
    lines.filter(l -> l.contains("ERROR")).forEach(System.out::println);
}

// Classic
try (BufferedReader br = Files.newBufferedReader(path)) {
    String line;
    while ((line = br.readLine()) != null) { }
}
```

> [!warning] `Files.lines()` returns a stream backed by an open file handle — you **must** close it with try-with-resources.

---

## ❓ Q564. How do you write a file?

```java
Files.writeString(path, "hello");                          // Java 11
Files.write(path, lines);
Files.writeString(path, "more", StandardOpenOption.APPEND);
try (BufferedWriter w = Files.newBufferedWriter(path)) { w.write("x"); }
```

---

## ❓ Q565. What is `PrintWriter` vs `PrintStream`?

`PrintStream` is byte-based (`System.out`); `PrintWriter` is character-based and preferred for text. Both swallow `IOException` by default — call `checkError()` if it matters. ⚠️

---

## ❓ Q566. What does `flush()` do and when do you need it?

Forces buffered data out to the destination. `close()` flushes automatically, but you need explicit `flush()` for long-lived streams (sockets, logs) where the receiver waits for data. 🚰

---

## ❓ Q567. What is `System.in`, `out`, `err`?

Standard input/output/error streams. They can be redirected with `System.setOut(...)`. `System.err` is unbuffered so errors appear immediately.

---

## ❓ Q568. `Scanner` vs `BufferedReader`? ⭐

| | `Scanner` | `BufferedReader` |
|---|-----------|------------------|
| Parses types | ✅ `nextInt()`, `nextDouble()` | ❌ strings only |
| Buffer size | small (1 KB) | large (8 KB) |
| Speed | slower (regex-based) | **faster** ✅ |
| Thread safe | ❌ | ✅ synchronized |

For competitive programming and large input, `BufferedReader` wins.

> [!warning] Classic `Scanner` trap: `nextInt()` leaves the newline in the buffer, so the next `nextLine()` returns an empty string. Call an extra `nextLine()` to consume it.

---

## ❓ Q569. What is the `File` class and its limits?

Old API for paths and metadata. Weaknesses: poor error messages (methods just return `false`), no symlink support, no file attributes, no atomic operations. **Replaced by `java.nio.file.Path` + `Files`.** ✅

---

## ❓ Q570. What is `try-with-resources` for I/O?

The correct way to close streams — see Part 4, Q256. Never rely on `finally { stream.close(); }` written by hand.

---

# ⚡ Section 2 — NIO & Files (Q571–Q580)

## ❓ Q571. What is NIO and how does it differ from IO? ⭐⭐

| | IO (`java.io`) | NIO (`java.nio`) |
|---|---------------|------------------|
| Model | **stream** oriented | **buffer** oriented |
| Blocking | blocking only | ✅ **non-blocking** possible |
| Core abstractions | streams | **Channels + Buffers + Selectors** |
| Direction | one-way | channels are bidirectional |
| Best for | simple sequential files | high-concurrency servers, large files |

---

## ❓ Q572. What is a `Channel` and a `Buffer`?

- **Channel** — a connection to a file, socket, or device; you read *into* buffers and write *from* buffers
- **Buffer** — a fixed-size memory block with `position`, `limit`, `capacity`; `flip()` switches from writing to reading

```java
ByteBuffer buf = ByteBuffer.allocate(1024);
channel.read(buf);
buf.flip();           // ⭐ prepare for reading
while (buf.hasRemaining()) System.out.print((char) buf.get());
buf.clear();
```

---

## ❓ Q573. What is a `Selector`?

One thread can monitor **many** channels for readiness (**multiplexing**) — the foundation of non-blocking servers like Netty. Instead of one thread per connection, one thread handles thousands. 🚀

---

## ❓ Q574. What is `Path` vs `File`?

```java
Path p = Paths.get("/home/user/f.txt");     // or Path.of(...) in Java 11
p.getFileName(); p.getParent(); p.toAbsolutePath(); p.normalize();
p.resolve("child.txt");  p.relativize(other);
File f = p.toFile();  Path back = f.toPath();   // interop
```

---

## ❓ Q575. What can the `Files` utility class do?

```java
Files.exists(p);  Files.size(p);  Files.isDirectory(p);
Files.createDirectories(p);  Files.createFile(p);
Files.copy(src, dst, StandardCopyOption.REPLACE_EXISTING);
Files.move(src, dst, StandardCopyOption.ATOMIC_MOVE);
Files.delete(p);        // throws if missing
Files.deleteIfExists(p);
Files.list(dir);        // 1 level, must be closed
Files.walk(dir);        // recursive, must be closed
Files.find(dir, depth, (path, attrs) -> ...);
Files.probeContentType(p);
Files.getLastModifiedTime(p);
```

---

## ❓ Q576. What is a memory-mapped file?

```java
MappedByteBuffer mb = channel.map(READ_WRITE, 0, size);
```
The OS maps the file directly into virtual memory — reads/writes bypass the usual copy into JVM heap. Extremely fast for very large files. Used by databases and message brokers. 🗺️

---

## ❓ Q577. What is `WatchService`?

Native OS file-change notifications — detect create/modify/delete without polling.

---

## ❓ Q578. What is a direct `ByteBuffer`?

`ByteBuffer.allocateDirect()` allocates **off-heap** memory that the OS can use for zero-copy I/O. Faster for I/O, but allocation is expensive and it is not managed by the normal GC — leaks are possible. ⚠️

---

## ❓ Q579. What is zero-copy?

`FileChannel.transferTo()` moves data directly from a file to a socket in the kernel, without copying it into user space. This is how high-performance file servers work. ⚡

---

## ❓ Q580. `Files.walk()` vs `Files.list()`?

`list()` = one level, `walk()` = recursive with an optional depth limit. Both return lazy streams holding OS resources → **always close them**.

---

# 📦 Section 3 — Serialization (Q581–Q596)

## ❓ Q581. What is serialization? ⭐

Converting an object into a byte stream so it can be stored or transmitted, and reconstructed later (deserialization).

```java
class Person implements Serializable {      // marker interface
    private static final long serialVersionUID = 1L;
}

try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("p.ser"))) {
    out.writeObject(person);
}
try (ObjectInputStream in = new ObjectInputStream(new FileInputStream("p.ser"))) {
    Person p = (Person) in.readObject();
}
```

---

## ❓ Q582. What is `serialVersionUID` and why does it matter? ⭐⭐

A version identifier for the class. During deserialization, the JVM compares the stored UID with the current class's UID — if they differ, it throws `InvalidClassException`.

If you do not declare it, the compiler **generates** one from the class structure. Then any small change (adding a method!) changes the UID and breaks compatibility with old data. **Always declare it explicitly.** ✅

---

## ❓ Q583. What is `transient`? ⭐

Marks a field to be **skipped** during serialization. On deserialization it gets the default value (`null`/0).

**Use for:** passwords, caches, derived values, non-serializable references, database connections, loggers.

```java
private transient String password;
private transient Connection conn;
```

---

## ❓ Q584. Are `static` fields serialized?

**No.** They belong to the class, not the instance. After deserialization they hold whatever the current JVM has.

---

## ❓ Q585. What happens if a field's type is not serializable?

`NotSerializableException` at runtime — unless the field is `transient`. Serialization is **deep**: the whole object graph must be serializable.

---

## ❓ Q586. What if the parent class is not serializable but the child is? ⭐

Deserialization calls the **parent's no-argument constructor** to initialize the inherited fields. If the parent has no accessible no-arg constructor → `InvalidClassException`.

Note the child's own constructor is **not** called at all during deserialization.

---

## ❓ Q587. Does deserialization call the constructor?

**No** for the serializable class itself — the object is created without running its constructor. That is exactly why serialization can **break invariants** and singletons. ⚠️

---

## ❓ Q588. How do you protect a singleton from serialization?

```java
private Object readResolve() { return INSTANCE; }   // replaces the deserialized object
```
Or use an `enum` singleton, which the JVM handles correctly for free. ✅ (Part 2, Q150)

---

## ❓ Q589. What are `writeObject` / `readObject`?

Private hooks for custom serialization logic:

```java
private void writeObject(ObjectOutputStream out) throws IOException {
    out.defaultWriteObject();
    out.writeUTF(encrypt(password));     // e.g. encrypt a transient field
}
private void readObject(ObjectInputStream in) throws IOException, ClassNotFoundException {
    in.defaultReadObject();
    this.password = decrypt(in.readUTF());
    // ⭐ also re-validate invariants here — deserialization bypasses the constructor
}
```

---

## ❓ Q590. `Serializable` vs `Externalizable`? ⭐

| | `Serializable` | `Externalizable` |
|---|----------------|------------------|
| Control | JVM handles it | **you** write `writeExternal`/`readExternal` |
| Constructor on read | not called | **public no-arg constructor IS called** |
| Performance | slower, more metadata | faster, compact |
| Effort | zero | full manual work |

---

## ❓ Q591. Why is Java serialization considered dangerous? ⭐⭐

- 🚨 **Deserialization of untrusted data is a major security hole** — gadget chains can achieve remote code execution. It has caused many real CVEs.
- Constructors are bypassed → invariants broken
- Fragile versioning
- Verbose, slow format
- Ties your class structure to your wire format

**Recommendation (*Effective Java*, Item 85): avoid Java serialization entirely in new systems.** Use JSON (Jackson), Protobuf, or Avro. If you must accept it, use a **deserialization filter** (`ObjectInputFilter`, Java 9+). 🔒

---

## ❓ Q592. How do you deep-copy with serialization?

Serialize to a `ByteArrayOutputStream` and read back — every object in the graph is recreated. Simple, but slow and requires everything to be serializable. (Part 2, Q146)

---

## ❓ Q593. Is the order of fields important in serialization?

No — fields are written by name. But **removing** a field or changing its type breaks compatibility; adding a field is usually compatible (it deserializes as the default value).

---

## ❓ Q594. What is `ObjectInputFilter`?

A Java 9+ allow/deny list applied before deserializing, limiting classes, depth, and array sizes — the standard mitigation for deserialization attacks.

---

## ❓ Q595. Can you serialize a lambda?

Only if the target type is serializable (e.g. cast to `(Runnable & Serializable)`). It works but is fragile — the synthetic method name can change between compilations. Avoid.

---

## ❓ Q596. What alternatives exist to Java serialization?

JSON (Jackson, Gson), Protocol Buffers, Avro, Kryo, MessagePack, and simple record-to-DTO mapping. All are faster, cross-language, and far safer. ✅

---

# 🔍 Section 4 — Reflection (Q597–Q610)

## ❓ Q597. What is reflection? ⭐

The ability to inspect and manipulate classes, methods, and fields **at runtime**, without knowing them at compile time.

```java
Class<?> c = Class.forName("com.app.User");
Object obj = c.getDeclaredConstructor().newInstance();
Method m = c.getDeclaredMethod("setName", String.class);
m.setAccessible(true);                     // bypasses `private` 😈
m.invoke(obj, "Ali");
Field f = c.getDeclaredField("id");
f.setAccessible(true);
f.set(obj, 42);
```

---

## ❓ Q598. How do you get a `Class` object? Three ways.

```java
Class<?> c1 = String.class;             // compile-time, no initialization
Class<?> c2 = "hello".getClass();       // from an instance
Class<?> c3 = Class.forName("java.lang.String");  // runtime, INITIALIZES the class
```

---

## ❓ Q599. `getMethods()` vs `getDeclaredMethods()`? ⭐

| | `getMethods()` | `getDeclaredMethods()` |
|---|----------------|------------------------|
| Access | **public only** | all: private, protected, default, public |
| Inherited | ✅ includes inherited | ❌ this class only |

Same distinction for `getFields`, `getConstructors`.

---

## ❓ Q600. What are the real uses of reflection? ⭐

- **Frameworks**: Spring (DI, `@Autowired`), Hibernate (entity mapping), JUnit (finding `@Test` methods)
- JSON libraries mapping fields to keys (Jackson, Gson)
- IDEs, debuggers, code generators
- Dynamic proxies and AOP
- Plugin systems and `ServiceLoader`

You rarely write reflection yourself — but you use frameworks built on it every day.

---

## ❓ Q601. What are the disadvantages of reflection? ⭐

- 🐢 **Slower** — no JIT inlining, plus access checks (though much better since Java 9)
- ❌ **No compile-time safety** — typos become runtime `NoSuchMethodException`
- 🔓 **Breaks encapsulation** — `setAccessible(true)` defeats `private`
- 🧱 Breaks refactoring (renaming a field silently breaks reflective code)
- ⚠️ Restricted by the module system and security managers

---

## ❓ Q602. How did Java 9 modules affect reflection?

Strong encapsulation: reflective access to non-exported packages fails unless the module `opens` them. That is why you sometimes see `--add-opens java.base/java.lang=ALL-UNNAMED` in startup scripts. 🔒

---

## ❓ Q603. What is a dynamic proxy? ⭐

Creating an implementation of an interface at runtime — the mechanism behind Spring AOP, transactions, and mocking libraries.

```java
Object proxy = Proxy.newProxyInstance(
    loader, new Class[]{Service.class},
    (p, method, args) -> {
        System.out.println("before " + method.getName());
        Object result = method.invoke(realService, args);
        System.out.println("after");
        return result;
    });
```
Limitation: **interfaces only**. For classes, frameworks use CGLIB or ByteBuddy (subclassing).

---

## ❓ Q604. Can reflection break `final`?

For non-static fields, `setAccessible(true)` + `Field.set` historically worked, but the JIT may have already inlined the constant, giving inconsistent results. Java 17+ blocks it for records and hidden classes. **Never rely on it.** ⚠️

---

## ❓ Q605. How do you get generic type info via reflection?

Type arguments of variables are erased, but declarations keep signatures:
```java
Type t = field.getGenericType();
if (t instanceof ParameterizedType pt) {
    Type[] args = pt.getActualTypeArguments();   // e.g. String for List<String>
}
```
See Part 4, Q303.

---

## ❓ Q606. What is `MethodHandle` / `VarHandle`?

Modern, faster alternatives to reflection introduced with `invokedynamic`. `MethodHandle` is a typed, JIT-friendly reference to a method; `VarHandle` (Java 9) gives fine-grained memory access with atomic and volatile semantics — replacing `sun.misc.Unsafe`.

---

## ❓ Q607. What is `ServiceLoader`?

The standard SPI mechanism: implementations declared in `META-INF/services` (or `provides ... with` in a module) are discovered at runtime.

```java
ServiceLoader.load(PaymentProvider.class).forEach(p -> p.register());
```

---

## ❓ Q608. How does Spring use reflection?

Scans classes for annotations, instantiates beans via reflective constructors, injects fields/setters, and wraps beans in dynamic proxies for transactions and AOP. Knowing this connects core Java to framework knowledge — interviewers love that bridge. 🌉

---

## ❓ Q609. Is reflection thread-safe?

`Class` objects are thread-safe, but `setAccessible` mutates shared `AccessibleObject` state, and your reflective target may not be thread-safe. Cache `Method` objects (that is what frameworks do for performance), but be careful with accessibility flags.

---

## ❓ Q610. How do frameworks make reflection fast?

They **cache** the reflective lookups (Method/Field objects) at startup, use `MethodHandle`s, or **generate bytecode** at build/startup time (Micronaut, Quarkus do exactly this to avoid runtime reflection and enable native images).

---

# 🏷️ Section 5 — Annotations (Q611–Q620)

## ❓ Q611. What is an annotation?

Metadata attached to code. It does not change behaviour by itself — a processor, compiler, or framework reads it and acts.

---

## ❓ Q612. What are the built-in annotations? ⭐

| Annotation | Purpose |
|---|---|
| `@Override` | compile-time check that you really override |
| `@Deprecated` | marks obsolete API (`since`, `forRemoval` in Java 9) |
| `@SuppressWarnings` | silence specific compiler warnings |
| `@FunctionalInterface` | enforce a single abstract method |
| `@SafeVarargs` | suppress generic varargs warnings |

---

## ❓ Q613. What are meta-annotations? ⭐

Annotations that annotate annotations:

| Meta-annotation | Meaning |
|---|---|
| `@Retention` | how long it is kept: `SOURCE`, `CLASS`, **`RUNTIME`** |
| `@Target` | where it can be applied: `TYPE`, `METHOD`, `FIELD`, `PARAMETER`, ... |
| `@Documented` | include in Javadoc |
| `@Inherited` | subclasses inherit it |
| `@Repeatable` | can appear multiple times (Java 8) |

---

## ❓ Q614. What are the retention policies? ⭐

| Policy | Kept in `.class`? | Visible via reflection? | Example |
|---|---|---|---|
| `SOURCE` | ❌ discarded by the compiler | ❌ | `@Override`, Lombok |
| `CLASS` (default) | ✅ | ❌ | bytecode tools |
| `RUNTIME` | ✅ | ✅ | Spring, JUnit, Jackson |

**If a framework needs to read it at runtime, it must be `RUNTIME`.** This is a very common interview question. ⭐

---

## ❓ Q615. How do you create a custom annotation?

```java
@Retention(RetentionPolicy.RUNTIME)
@Target({ElementType.METHOD, ElementType.TYPE})
public @interface Loggable {
    String value() default "";           // `value` can be used without a name
    int timeoutMs() default 1000;
    String[] tags() default {};
}

@Loggable("audit")
public void transfer() { }
```

**Allowed member types:** primitives, `String`, `Class`, enums, other annotations, and arrays of these. No arbitrary objects, no null defaults.

---

## ❓ Q616. How do you read annotations at runtime?

```java
if (method.isAnnotationPresent(Loggable.class)) {
    Loggable a = method.getAnnotation(Loggable.class);
    System.out.println(a.value() + " " + a.timeoutMs());
}
```

---

## ❓ Q617. What is annotation processing (APT)?

Compile-time code generation via `javax.annotation.processing` — used by Lombok, MapStruct, Dagger, and immutables. It runs during `javac`, generating source files before compilation completes. Faster than runtime reflection and native-image friendly. ⚡

---

## ❓ Q618. Can annotations be inherited?

Only class-level annotations marked `@Inherited`, and only for class inheritance — **method annotations are never inherited**. That is why Spring checks the whole hierarchy manually.

---

## ❓ Q619. What are type annotations? (Java 8)

Annotations on any type use, enabling static analysis tools like the Checker Framework:
```java
@NonNull String name;
List<@NonNull String> names;
```

---

## ❓ Q620. Do annotations affect performance?

`SOURCE` and `CLASS` retention: zero runtime cost. `RUNTIME` retention: only costs when something reflectively reads them — usually at startup, then cached.

---

# 🧩 Section 6 — Quick Fire Round

> [!question]- Which class should you use to read a text file line by line?
> `BufferedReader` (or `Files.lines()` / `Files.newBufferedReader`).

> [!question]- Is `Serializable` a marker interface?
> Yes — no methods.

> [!question]- What happens if `serialVersionUID` does not match?
> `InvalidClassException`.

> [!question]- Are transient fields restored after deserialization?
> No — they get default values (null/0/false).

> [!question]- Does deserialization run the constructor?
> Not for the serializable class; the first non-serializable superclass constructor does run.

> [!question]- What is the default charset problem?
> Platform-dependent encoding causing different behaviour per machine. Always specify UTF-8 (default since Java 18).

> [!question]- Can reflection access private members?
> Yes, with `setAccessible(true)` — subject to module restrictions.

> [!question]- Which retention policy do Spring and JUnit annotations use?
> `RUNTIME`.

> [!question]- What is the difference between `Class.forName()` and `.class`?
> `forName` loads and **initializes**; `.class` does not trigger initialization.

> [!question]- Why is `Files.lines()` risky?
> It holds an open file handle — must be closed with try-with-resources.

> [!question]- Which is faster: `Scanner` or `BufferedReader`?
> `BufferedReader`.

> [!question]- What replaced `sun.misc.Unsafe` for atomic field access?
> `VarHandle` (Java 9).

---

## 🎓 Self-Test Checklist for Part 8

- [ ] I know when to use byte streams vs character streams
- [ ] I can explain why buffering matters and by how much
- [ ] I always specify the charset explicitly
- [ ] I can explain `serialVersionUID` and `transient`
- [ ] I can explain why Java serialization is a security risk and what to use instead
- [ ] I can protect a singleton with `readResolve()`
- [ ] I know the difference between `getMethods` and `getDeclaredMethods`
- [ ] I can explain how Spring uses reflection and proxies
- [ ] I know the three retention policies and which frameworks need RUNTIME

---

> [!success] ✅ Part 8 complete — Q557–Q620
> 👉 Next: [[01 - Java/Interview/09 - Patterns & Puzzles|Part 9 — Patterns & Puzzles]]

#java #interview #core-java #io #reflection #part8
