**Polymorphism** is a core concept in **object-oriented programming (OOP)** that allows objects of different classes to be treated as objects of a common superclass or interface. The term means "many forms," and it enables **flexibility** and **code reusability** by letting one interface or method work with different data types or classes. In Java, polymorphism is implemented in two ways:

1. **Compile-Time Polymorphism (Static Binding)**
    
2. **Runtime Polymorphism (Dynamic Binding)**
    

---

### **1. Compile-Time Polymorphism (Method Overloading)**

This is achieved through **method overloading**, where multiple methods in the same class have the **same name** but **different parameters** (type, number, or order). The compiler determines which method to call based on the arguments provided.

**Example**:

java

Copy

class Calculator {
    // Method 1: Adds two integers
    int add(int a, int b) {
        return a + b;
    }
    
    // Method 2: Adds three integers (overloaded)
    int add(int a, int b, int c) {
        return a + b + c;
    }
    
    // Method 3: Adds two doubles (overloaded)
    double add(double a, double b) {
        return a + b;
    }
}

// Usage:
Calculator calc = new Calculator();
calc.add(2, 3);       // Calls method 1
calc.add(2, 3, 4);    // Calls method 2
calc.add(2.5, 3.5);   // Calls method 3

**Key Points**:

- Resolved at **compile time**.
    
- Return type alone doesn’t differentiate overloaded methods.
    

---

### **2. Runtime Polymorphism (Method Overriding)**

This is achieved through **method overriding**, where a subclass provides a **specific implementation** of a method already defined in its superclass or interface. The JVM determines which method to execute **at runtime** based on the **actual object type** (not the reference type).

**Example**:

java

Copy

class Animal {
    void makeSound() {
        System.out.println("Animal makes a sound");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() { // Overridden method
        System.out.println("Dog barks");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() { // Overridden method
        System.out.println("Cat meows");
    }
}

// Usage:
Animal myAnimal = new Dog();
myAnimal.makeSound(); // Output: "Dog barks" (Runtime decision)

Animal anotherAnimal = new Cat();
anotherAnimal.makeSound(); // Output: "Cat meows"

**Key Points**:

- Requires **inheritance** (subclassing) or **interface implementation**.
    
- The `@Override` annotation ensures correct overriding (optional but recommended).
    
- The method signature (name, parameters, return type) must match the parent method.
    
- Uses **dynamic method dispatch** (JVM decides which method to call at runtime).
    

---

### **How Java Implements Runtime Polymorphism**

Java uses **method tables** (v-tables) internally to track overridden methods. When a method is called on a superclass reference pointing to a subclass object, the JVM checks the **actual object’s type** and executes the corresponding overridden method.

---

### **Key Use Cases**

1. **Flexible method invocation**: Treat all subclasses as their superclass type (e.g., `Animal` reference for `Dog`/`Cat` objects).
    
2. **Code reusability**: Write generic code that works with multiple classes (e.g., `List` interface for `ArrayList`, `LinkedList`).
    
3. **Interchangeable components**: Swap implementations without changing existing code (e.g., different database drivers).
    

---

### **Important Notes**

- **Static methods** cannot be overridden (they’re bound at compile time).
    
- **Private/final methods** cannot be overridden.
    
- **Variables** are not polymorphic (they follow reference type, not object type).
    

Polymorphism is foundational in Java for building scalable, maintainable systems (e.g., Spring Boot dependency injection relies heavily on it!). 😊