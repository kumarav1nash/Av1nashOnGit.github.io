Q1. **Is it possible to add three objects of the same Employee class (e1, e2, e3) and two objects of the Department class (d1, d2) to a TreeSet? What will happen if I attempt to print those objects using System.out.println?**

Ans :- We need to introduce custom coparator which compare employee and dept and pass while creating treeset, other wise two separate treeset is always an option

```
  
public class TreeSetExample {  
    public static void main(String[] args) {  
        TreeSet<Object> treeSet = new TreeSet<>(new CustomComparator());  
  
        Employee e1 = new Employee(101, "John");  
        Employee e2 = new Employee(102, "Alice");  
        Employee e3 = new Employee(103, "Bob");  
  
        Department d1 = new Department(201, "HR");  
        Department d2 = new Department(202, "IT");  
        Employee e4 = new Employee(303,"BOBA");  
        treeSet.add(e1);  
        treeSet.add(e2);  
        treeSet.add(e3);  
        treeSet.add(d1);  
        treeSet.add(d2);  
        treeSet.add(e4);  
  
        System.out.println("Elements in TreeSet:");  
        for (Object obj : treeSet) {  
            System.out.println(obj);  
        }  
    }  
}


class CustomComparator implements Comparator<Object> {  
    @Override  
    public int compare(Object o1, Object o2) {  
        if (o1 instanceof Employee && o2 instanceof Employee) {  
            return ((Employee) o1).compareTo((Employee) o2);  
        } else if (o1 instanceof Department && o2 instanceof Department) {  
            return ((Department) o1).compareTo((Department) o2);  
        } else if (o1 instanceof Employee) {  
            return -1; // Define consistent ordering between Employee and Department  
        } else {  
            return 1; // Define consistent ordering between Department and Employee  
        }  
    }  
}
```

Q2. **When to use comparable and comparator in Java?**
In Java Both used to compare two objects, however they serve different purpose

**Comparable Interface** 
*Natural Sorting Order*: Comparable is used when you want to define a natural ordering for objects of a class. This means that the class itself defines how its instances should be compared.

*Single Sorting Order*: With Comparable, there is only one way to compare objects. The sorting logic is baked into the class itself via the compareTo() method.

*Intrinsic Implementation*: You implement Comparable in the class whose instances you want to sort. This allows for consistent sorting behavior across all collections that use natural ordering.
Example: Sorting String, Integer, or custom classes like Employee based on their ID, name, or any other intrinsic property.

**_Comparator Interface_**
*Custom Sorting Order*: Comparator is used when you want to define multiple sorting orders for objects of a class or when you don’t have access to the class’s source code to implement Comparable.

*External Sorting Logic*: With Comparator, you can define sorting logic externally to the class being sorted. This is useful when you want to sort objects based on different criteria without modifying their original class.

*Multiple Sorting Orders*: You can define multiple Comparator implementations to sort objects differently as needed, without modifying the class itself.

Example: Sorting Employee objects based on their salary, age, or any other criteria that may vary depending on the context.

**_When to Use Which?_**  
Use Comparable when you have a natural sorting order that’s intrinsic to the class itself and you want all instances of the class to be sorted in the same way.

Use Comparator when you need custom sorting logic, or when you want to sort objects in multiple ways without altering their original class, or when you’re dealing with classes from external libraries that you can’t modify.

Q3.  **“How can we determine if the current code incorporates aggregation, composition, and inheritance, and what practical purposes do these concepts serve?”**

To determine if the current code incorporates aggregation, composition, and inheritance, and to understand their practical applications, you’ll need to review the relationships between objects and classes within the codebase. Here’s how to approach this:

**_1. Identify Inheritance:_**  
Inheritance is a “is-a” relationship between a base class (parent) and a derived class (child), where the child class inherits properties and behaviors (methods) from the parent class and may add or override them.

**_How to Check_**:Look for class definitions to see if any class is extending another class.  
Keywords to spot: In Java and similar languages, extends for class inheritance and implements for interface implementation.  
**_Practical Use_**:Inheritance is used for code reuse and polymorphism. It allows derived classes to reuse code from their base classes, reducing redundancy. For example, a Vehicle class could be a base class, and Car and Motorcycle could be derived classes, inheriting properties like speed and methods like move().  

**_2. Spot Aggregation_**:  
Aggregation implies a “has-a” relationship where one class contains references to others but does not exclusively control their lifecycle.

**_How to Check_**:Look for classes that hold references to other class instances as member variables but don’t instantiate them within their own constructors.  
The contained objects can be passed to the aggregating object’s constructor, or set via setters.  

*Practical Use: Aggregation is useful for representing relationships where components can belong to multiple containers. For instance, a Professor and Student class might aggregate a Department class, indicating both can be associated with the same department.*

**_3. Determine Composition:_**  
Composition is a stronger form of aggregation with ownership, implying a “part-of” relationship. The lifecycle of the contained objects depends on the lifecycle of the container object.

**_How to Check:_** Classes that create instances of other classes within their own constructors or methods, and manage their lifetime, exhibit composition.  
If the container class is destroyed, the contained objects are also destroyed.**_Practical Use:_** Composition is used to model relationships where components shouldn’t exist without their container. For instance, a Page class might be a component of a Book class; if the book is destroyed, so are its pages.

Q4. **What is a Memory leak in Java?**
A memory leak in Java occurs when objects that are no longer needed by the application still occupy memory because the garbage collector cannot remove them from working memory. This situation typically happens when references to these objects remain in the code, preventing the garbage collector from deallocating the memory they occupy, despite them being effectively useless for the application’s further operations.

Q5. **What is OutOfMemoryError and How to solve it?**
**_Symptoms_**

- Sudden failure or major slowness of your application
- Error found in log and console -java.lang.OutOfMemoryError: Java heap space
- High usage of cpu due to increased java garbage collector activity

Possible root causes

- Inadequate heap space capacity settings eg.xms,xmx
- Java program memory leaks
- Excessive application memory footprint and processing workload

**_Diagnostic tools_**

- Jvm verbose:gc logs
- Java visual vm, oracle mision control
- Apm technologies

**Solution**

- Increase the max heap capacity using xmx parameter
- Monitor profile and resolve application memory leaks
- Optimise and reduce your java application memory footprint
- Split the workload of your java application to several process
- We can ask hotspot jvm to generate heap dump
- Gc log


Q6. **How to create an immutable class, like String?**

- **Make the class final**:
    - This prevents other classes from inheriting from it and potentially altering its behavior.
- **Make all fields private and final**:
    - This ensures that fields are not accessible directly and cannot be modified after initialization.
- **Provide a constructor for all fields**:
    - This is the only way to set the values of the fields. Ensure that no setter methods are provided.
- **Avoid methods that modify fields**:
    - Ensure that methods in the class do not modify the state of the object.
- **If the class has fields that are references to mutable objects, return copies of these objects in getters**:
    - This prevents callers from modifying the internal state of the object through mutable references.
- **Ensure proper handling of mutable fields**:
    - If any field is a mutable object, ensure that the original object cannot be altered externally.

### Example: Immutable Class
Here's an example of an immutable class in Java:

```
import java.util.Date;

public final class ImmutablePerson {

    private final String name;
    private final int age;
    private final Date birthDate;

    // Constructor to initialize all fields
    public ImmutablePerson(String name, int age, Date birthDate) {
        this.name = name;
        this.age = age;
        // Create a new Date object to ensure the original birthDate cannot be modified
        this.birthDate = new Date(birthDate.getTime());
    }

    // Getter methods
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public Date getBirthDate() {
        // Return a new Date object to ensure the internal birthDate cannot be modified
        return new Date(birthDate.getTime());
    }

    // No setter methods
    // No methods that modify fields
}

```