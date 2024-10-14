
**1. Introduction to Object-Oriented Programming (OOP) Concepts**

#### Benefits of OOP and its Principles:
- Modularity: Organizing code into manageable components.
- Reusability: Reusing code and designing generic solutions.
- Maintainability: Easily updating and maintaining code.
- Scalability: Handling larger projects through object-oriented design.
#### Understanding Abstraction, Encapsulation, Inheritance, and Polymorphism:
- Abstraction: Hiding unnecessary details and exposing essential features.
- Encapsulation: Wrapping data and methods into a single unit (class) to control access.
- Inheritance: Deriving new classes from existing ones to promote code reuse.
- Polymorphism: Using the same interface to represent different data types.

**2. Inheritance and Polymorphism**

#### Extending Classes and Creating Subclasses:
- Defining superclasses and subclasses.
- The `extends` keyword for inheritance.
- Example:
```
class Animal {

	void sound() {
		System.out.println("Animal makes a sound.");
		}
	} 
	 
class Dog extends Animal {

	void sound() {         
		System.out.println("Dog barks.");     
	} 
	
}  

public class Main {     
	public static void main(String[] args) {         
		Animal animal = new Dog();         
		animal.sound(); // Output: Dog barks.     
	}
}
```
#### Method Overriding and Polymorphic Behaviour:
- Overriding methods in subclasses.
- Achieving polymorphism using dynamic method dispatch.
- Example:
 ```
 class Shape {
    void draw() {
	    System.out.println("Drawing a shape.");
    } 
}

class Circle extends Shape {
	void draw() {
		System.out.println("Drawing a circle.");     
	} 
}  

class Square extends Shape {     
	void draw() {         
		System.out.println("Drawing a square.");     
	} 
}  

public class Main {     
	public static void main(String[] args) {         
		Shape shape1 = new Circle();         
		Shape shape2 = new Square();          
		shape1.draw(); // Output: Drawing a circle.         
		shape2.draw(); // Output: Drawing a square.     
	} 
}
```
**3. Encapsulation and Data Hiding**

#### Access Modifiers and Data Hiding Techniques:
- Access modifiers (public, private, protected, default).
- Encapsulating data using private access modifier.
- Getter and setter methods for controlled access to data.
- Example:
 ```
 class Person {
    private String name;     
    private int age;      
    public String getName() {
	    return name;     
	}      
    
    public void setName(String name) {
	    this.name = name;     
    }
             
    public int getAge() {
	    return age;     
    }   
    
	public void setAge(int age) {
		if (age > 0) {
			this.age = age;         
		} else {             
			System.out.println("Age cannot be negative.");         
		}
	}
}

public class Main {     
	public static void main(String[] args) {         
		Person person = new Person();         
		person.setName("John");         
		person.setAge(-30); //Output: Age cannot be negative
		System.out.println(person.getName()); //Output: John
		System.out.println(person.getAge()); // Output: 0 (due to invalid age)     
	} 
}
```
**4. Abstraction and Interfaces**

#### Abstract Classes and Methods:
- Defining abstract classes and abstract methods.
- Implementing abstract methods in subclasses.
- Example:
```
abstract class Shape {     
	abstract void draw(); 
}

class Circle extends Shape {     
	void draw() {         
		System.out.println("Drawing a circle.");     
	}
}

public class Main {     
	public static void main(String[] args) {         
		Shape shape = new Circle();
		shape.draw(); // Output: Drawing a circle.     
	}
}
```
#### Implementing Interfaces for Multiple Inheritance:
- Declaring interfaces and their methods.
- A class implementing multiple interfaces.
- Example:
 ```
 
interface Walkable {     
	void walk(); 
}

interface Swimmable {     
	void swim(); 
}
 
class Human implements Walkable, Swimmable {     
	public void walk() {         
		 System.out.println("Human can walk.");     
	}      
	public void swim() {         
		System.out.println("Human can swim.");     
	}
 
}
 
public class Main {      
	public static void main(String[] args) {         
		Human person = new Human();        
		person.walk(); // Output: Human can walk.         
		person.swim(); // Output: Human can swim.     
	}
}
```
**5. Generics and File Handling**

#### Introduction to Java Generics:
- Writing generic classes and methods.
- Benefits of using generics for type safety.
- Example:
```
class Box<T> {  
	private T value;      
	public void setValue(T value) {  
		this.value = value;     
	} 
	public T getValue() {         
		return value;     
	}
}

public class Main {     
	public static void main(String[] args) {         
	Box<Integer> integerBox = new Box<>();         
	integerBox.setValue(10);         
	int value = integerBox.getValue(); // No casting needed.         
	System.out.println(value); // Output: 10     
	}
}
```
#### Reading and Writing Files in Java:
- Using `FileInputStream` and `FileOutputStream` for reading and writing binary files.
- Using `FileReader` and `FileWriter` for reading and writing text files.
- Example:
```
import java.io.*;  

public class Main {     
	public static void main(String[] args) {         
		try {             // Writing to a file
			FileWriter writer = new FileWriter("output.txt");             
			writer.write("Hello, File Handling!");
			writer.close();              // Reading from a file             
			FileReader reader = new FileReader("output.txt");             
			int character;             
			while ((character = reader.read()) != -1) {
				System.out.print((char) character); // Output: Hello, File Handling!       
			}
			reader.close();         
		} catch (IOException e) {  
			e.printStackTrace();
		}
	}
}
```