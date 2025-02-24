Java 8 introduced groundbreaking features that revolutionized how developers write code, emphasizing **functional programming**, **simplicity**, and **performance**. Here’s a structured breakdown of the key features with **examples** and **use cases**:

---

### **1. Lambda Expressions**

**What**: Concise syntax for writing anonymous functions.  
**Why**: Enable functional-style programming and simplify code for interfaces with a single method (functional interfaces).

**Example**:

```java
// Before Java 8: Anonymous inner class
Runnable r = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello World");
    }
};

// Java 8: Lambda expression
Runnable r = () -> System.out.println("Hello World");
```

**Use Case**: Event handling, thread initialization, Streams API.

---

### **2. Streams API**

**What**: A declarative way to process collections (filter, map, reduce).  
**Why**: Enables parallel processing, improves readability, and avoids boilerplate loops.

**Example**:
```java

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squares = numbers.stream()
                               .filter(n -> n % 2 == 0)
                               .map(n -> n * n)
                               .collect(Collectors.toList());
// Output: [4, 16]
```

**Key Operations**:
- **Filter**: `filter(Predicate)`
- **Transform**: `map(Function)`
- **Aggregate**: `reduce()`, `collect()`
- **Short-circuit**: `findFirst()`, `anyMatch()`

**Use Case**: Batch processing of data, database queries, and transformations.

---

### **3. Optional Class**

**What**: A container to avoid `NullPointerException` by explicitly handling null values.  
**Why**: Forces developers to check for nulls and write safer code.

**Example**:
```java

Optional<String> name = Optional.ofNullable(getNameFromDB());
String result = name.orElse("default");
// If name is null, returns "default"
```

**Methods**:
- `orElse()`, `orElseGet()`, `orElseThrow()`
- `isPresent()`, `ifPresent(Consumer)`

**Use Case**: Database results, API responses, and method return values.

---

### **4. Default and Static Methods in Interfaces**

**What**: Interfaces can have method implementations using `default` and `static` keywords.  
**Why**: Evolve interfaces without breaking existing implementations.

**Example**:
```java
interface Vehicle {
    // Default method
    default void start() {
        System.out.println("Vehicle started");
    }

    // Static method
    static void stop() {
        System.out.println("Vehicle stopped");
    }
}

class Car implements Vehicle {}

// Usage:
Car car = new Car();
car.start();          // Calls default method
Vehicle.stop();       // Calls static method
```

**Use Case**: Backward compatibility (e.g., adding `stream()` to `Collection` in Java 8).

---

### **5. Method References**

**What**: Shorthand syntax to call existing methods using `::`.  
**Why**: Simplify lambda expressions when calling existing methods.

**Example**:
```java
List<String> names = Arrays.asList("Alice", "Bob");
names.forEach(System.out::println); // Equivalent to (s) -> System.out.println(s)
```

**Types**:

- Static method: `ClassName::methodName`
- Instance method: `instance::methodName`
- Constructor: `ClassName::new`


**Use Case**: Reusing existing methods in Streams and lambdas.

---

### **6. New Date and Time API (`java.time`)**

**What**: Immutable, thread-safe classes like `LocalDate`, `LocalTime`, and `ZonedDateTime`.  
**Why**: Fixes thread-safety and design flaws in legacy `Date`/`Calendar` classes.

**Example**:
```java
LocalDate date = LocalDate.now();
LocalDate nextWeek = date.plusDays(7);

DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
String formatted = date.format(formatter); // e.g., "25-10-2023"
```

**Key Classes**:
- `LocalDate`, `LocalTime`, `LocalDateTime`
- `Period`, `Duration`
- `ZonedDateTime` (for time zones)

**Use Case**: Scheduling, event management, and financial calculations.

---

### **7. Functional Interfaces**

**What**: Interfaces with **exactly one abstract method** (e.g., `Predicate`, `Function`, `Consumer`).  
**Why**: Provide target types for lambda expressions.

**Example**:
```java
// Predicate: returns boolean
Predicate<Integer> isEven = n -> n % 2 == 0;
System.out.println(isEven.test(4)); // true

// Function: transforms input
Function<String, Integer> length = String::length;
System.out.println(length.apply("Java")); // 4
```

**Common Interfaces**:

- `Predicate<T>`: `test(T) -> boolean`
- `Function<T, R>`: `apply(T) -> R`
- `Consumer<T>`: `accept(T) -> void`
- `Supplier<T>`: `get() -> T`

**Use Case**: Streams, custom lambda logic.

---

### **8. Parallel Streams**

**What**: Process data concurrently using `parallelStream()`.  
**Why**: Leverage multi-core CPUs for faster bulk operations.

**Example**:
```java

List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
int sum = numbers.parallelStream()
                 .mapToInt(n -> n)
                 .sum();
```

**Caution**: Use only for large datasets or CPU-intensive tasks (overhead for small data).

---

### **9. Nashorn JavaScript Engine**

**What**: A faster JavaScript engine (replaced Rhino).  
**Why**: Execute JS code within Java applications.

**Example**:
```java
ScriptEngine engine = new ScriptEngineManager().getEngineByName("nashorn");
engine.eval("print('Hello from JavaScript!')");
```

**Use Case**: Scripting, dynamic configurations.

---

### **10. Type Annotations and Repeating Annotations**

**What**: Annotations can be applied to types (e.g., `List<@NonNull String>`) and repeated.  
**Why**: Improved static analysis and code validation.

**Example**:
```java
@Repeatable(Checks.class)
@interface Check { String value(); }

@Check("security") @Check("performance")
class Application { ... }
```

**Use Case**: Frameworks (e.g., Spring, Hibernate) and custom validations.

---

### **Impact of Java 8**

- **Functional Programming**: Made Java competitive with Scala, Kotlin.
- **Readability**: Streams and lambdas reduced boilerplate.
- **Concurrency**: Parallel streams simplified multi-threading.
- **Modern APIs**: `java.time` and `Optional` fixed long-standing issues.

**Bonus**: The JVM’s **Metaspace** replaced PermGen for class metadata (reduces `OutOfMemoryError`).

---

Java 8 is a must-know for interviews (especially for Spring Boot roles) as it underpins modern Java development! 😊