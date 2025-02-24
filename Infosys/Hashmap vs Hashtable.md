**HashMap vs. Hashtable in Java**

|**Feature**|**HashMap**|**Hashtable**|
|---|---|---|
|**Synchronization**|Not synchronized (not thread-safe).|Synchronized (thread-safe).|
|**Null Keys/Values**|Allows **1 null key** and **multiple null values**.|**Prohibits null keys/values** (throws `NullPointerException`).|
|**Legacy/Modern**|Part of the modern Java Collections Framework (since Java 1.2).|Legacy class (since Java 1.0).|
|**Performance**|Faster in single-threaded scenarios (no synchronization overhead).|Slower due to synchronization.|
|**Iteration**|Uses `Iterator` (supports `remove()` method).|Uses `Enumeration` (legacy, no `remove()`).|
|**Inheritance**|Extends `AbstractMap`.|Extends `Dictionary` (obsolete).|
|**ConcurrentModification**|Fail-fast iterators (throws `ConcurrentModificationException`).|No fail-fast behavior.|
|**Use Cases**|Default choice for non-threaded environments.|Rarely used; prefer `ConcurrentHashMap` for thread safety.|

---

### **Key Differences Explained**

#### 1. **Thread Safety**

- **HashMap**: Not thread-safe. Use `ConcurrentHashMap` for concurrent environments.
    
- **Hashtable**: Synchronized methods (e.g., `put()`, `get()`) ensure thread safety but incur performance costs.
    

#### 2. **Null Handling**

- **HashMap**:
```java
    HashMap<String, Integer> map = new HashMap<>();
    map.put(null, 1);          // Allowed
    map.put("key", null);      // Allowed
```
    
- **Hashtable**:
    ```java
    
    Hashtable<String, Integer> table = new Hashtable<>();
    table.put(null, 1);        // Throws NullPointerException
    table.put("key", null);    // Throws NullPointerException
```
    

#### 3. **Performance**

- **HashMap** avoids synchronization overhead, making it faster for single-threaded apps.
    
- **Hashtable**’s synchronized methods slow it down but ensure thread safety.
    

#### 4. **Iteration**

- **HashMap** uses `Iterator` (modern, flexible):
    
    java
    
    Copy
    
    Iterator<Map.Entry<String, Integer>> it = map.entrySet().iterator();
    while (it.hasNext()) {
        it.remove(); // Supported
    }
    
- **Hashtable** uses `Enumeration` (legacy):
    
    java
    
    Copy
    
    Enumeration<Integer> e = table.elements();
    while (e.hasMoreElements()) {
        e.nextElement();
        // No remove() method
    }
    

#### 5. **Legacy vs. Modern**

- **Hashtable** predates the Java Collections Framework and is largely replaced by `HashMap` and `ConcurrentHashMap`.
    

---

### **When to Use Which?**

- **Use `HashMap`**:
    
    - Default choice for most applications.
        
    - Non-threaded environments or when using external synchronization.
        
- **Avoid `Hashtable`**:
    
    - Legacy codebases.
        
    - Use `ConcurrentHashMap` instead for thread safety with better performance.
        

---

### **Example Code**

java

Copy

// HashMap Example
HashMap<String, Integer> hashMap = new HashMap<>();
hashMap.put("A", 1);
hashMap.put(null, 2);       // Works
hashMap.put("B", null);     // Works

// Hashtable Example
Hashtable<String, Integer> hashtable = new Hashtable<>();
hashtable.put("A", 1);
// hashtable.put(null, 2);  // Throws NullPointerException
// hashtable.put("B", null);// Throws NullPointerException

---

### **Summary**

- **`HashMap`** is faster, flexible, and modern.
    
- **`Hashtable`** is legacy, thread-safe, and restrictive.
    
- Prefer **`ConcurrentHashMap`** over `Hashtable` for concurrent needs.