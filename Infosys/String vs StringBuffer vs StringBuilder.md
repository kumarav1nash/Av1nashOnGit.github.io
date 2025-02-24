In Java, `String`, `StringBuffer`, and `StringBuilder` are classes used to handle sequences of characters, but they differ significantly in terms of **mutability**, **thread safety**, and **performance**. Here's a structured comparison:

---

### **1. Mutability**

| **Class**       | **Mutability**                                                                                                            |
| --------------- | ------------------------------------------------------------------------------------------------------------------------- |
| `String`        | **Immutable**: Once created, its value cannot be modified. Every modification (e.g., concatenation) creates a new object. |
| `StringBuffer`  | **Mutable**: Content can be modified without creating new objects.                                                        |
| `StringBuilder` | **Mutable**: Same as `StringBuffer` but **not thread-safe** (introduced in Java 5).                                       |

---

### **2. Thread Safety**

|**Class**|**Thread Safety**|
|---|---|
|`String`|Thread-safe (immutability inherently makes it safe).|
|`StringBuffer`|**Thread-safe**: Methods are synchronized (safe for multi-threaded environments).|
|`StringBuilder`|**Not thread-safe**: No synchronization (faster in single-threaded contexts).|

---

### **3. Performance**

|**Class**|**Performance**|
|---|---|
|`String`|Slow for repeated modifications due to object creation overhead.|
|`StringBuffer`|Slower than `StringBuilder` (synchronization overhead) but safe for concurrency.|
|`StringBuilder`|Fastest for string manipulation in single-threaded scenarios.|

---

### **4. Use Cases**

|**Class**|**When to Use**|
|---|---|
|`String`|- When the value is constant or rarely changes (e.g., configuration keys).  <br>- For thread-safe read-only operations.|
|`StringBuffer`|- When thread safety is required for mutable operations (e.g., shared resources in multi-threaded apps).  <br>- Legacy code (pre-Java 5).|
|`StringBuilder`|- For mutable operations in single-threaded environments (e.g., building JSON/XML dynamically).  <br>- Default choice for efficient string manipulation.|

---

### **5. Key Methods**

All three classes support methods like `append()`, `insert()`, and `reverse()`, but:

- `StringBuffer` and `StringBuilder` provide **mutable operations** (e.g., `append()` modifies the object).
    
- `String` operations (e.g., `concat()`, `substring()`) return **new `String` objects**.
    

---

### **6. Examples**

#### **String (Immutable)**
```java
String str = "Hello";
str = str.concat(" World"); // Creates a new object
System.out.println(str); // "Hello World" (new object)
```

#### **StringBuffer (Mutable & Thread-Safe)**
```java
StringBuffer sbf = new StringBuffer("Hello");
sbf.append(" World"); // Modifies the same object
System.out.println(sbf); // "Hello World"
```

#### **StringBuilder (Mutable & Not Thread-Safe)**

```java
StringBuilder sbl = new StringBuilder("Hello");
sbl.append(" World"); // Modifies the same object
System.out.println(sbl); // "Hello World"
```

---

### **7. Memory Efficiency**

- **`String`**: Inefficient for repeated modifications (creates many intermediate objects).
    
- **`StringBuffer`/`StringBuilder`**: Avoid object creation overhead by modifying the same buffer.
    

---

### **Summary Table**

| **Feature**       | `String`         | `StringBuffer`      | `StringBuilder`      |
| ----------------- | ---------------- | ------------------- | -------------------- |
| **Mutability**    | Immutable        | Mutable             | Mutable              |
| **Thread Safety** | Yes (inherent)   | Yes (synchronized)  | No                   |
| **Performance**   | Slow for changes | Moderate            | Fastest              |
| **Use Case**      | Fixed values     | Multi-threaded apps | Single-threaded apps |

---

### **When to Choose Which?**

- **Use `String`** for constants or infrequent changes.
    
- **Use `StringBuffer`** for thread-safe mutable operations (rare in modern Java; prefer `ConcurrentHashMap` or other concurrent classes).
    
- **Use `StringBuilder`** for most mutable string operations (default choice for efficiency).
    

**Example in a Loop**:
```java
// Inefficient with String:
String result = "";
for (int i = 0; i < 1000; i++) {
    result += i; // Creates 1000 objects!
}

// Efficient with StringBuilder:
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb.append(i); // Modifies one object
}
```

---

### **Key Takeaway**

- **Prefer `StringBuilder`** for mutable string operations unless thread safety is explicitly required.
    
- **Avoid `String`** for heavy string manipulation (e.g., loops) to prevent performance issues.
    

Understanding these differences ensures efficient and thread-safe string handling in Java! 😊