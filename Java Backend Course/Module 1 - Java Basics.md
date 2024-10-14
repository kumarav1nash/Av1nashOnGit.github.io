**1. Introduction to Java**

- Java is a high-level, object-oriented programming language developed by Sun Microsystems (now owned by Oracle). Read more => [[The winding road from FORTRAN to Java]]
- It is platform-independent and follows the "Write Once, Run Anywhere" (WORA) principle.
- Java Virtual Machine (JVM) and platform independence
- **Javac** compiles the java code into bytecode and then **JVM** interpretes the bytecode into respective machince code depending on the system.
- Example:
```
 public class HelloWorld {     
	    public static void main(String[] args) {        
		     System.out.println("Hello, World!");     
	     } 
     }
```  

**2. Setting up the Development Environment**

- Download and install the Java Development Kit (JDK) from Oracle's website.
- Configure environment variables (PATH and JAVA_HOME) to run Java programs from the command line.
- Writing and running a simple "Hello, World!" program
- Example:
```
	public class HelloWorld {     
			public static void main(String[] args) {         
			System.out.println("Hello, World!");     
		} 
	}
```

**3. Fundamentals of Programming in Java**

- Basic Java syntax and structure
- Creating and running a Java program
- Java programs are organized into classes.
- Each program must have a `main` method as the entry point.
- Example:
```
public class MyFirstProgram {
	public static void main(String[] args) {
		System.out.println("This is my first Java program!");
	}
}
```
**4. Variables, Data Types, and Operators**

- Declaring and initialising variables
- Variables are used to store data in Java.
- Data types include int, double, char, boolean, etc.
- Arithmetic, relational, and logical operators are used to perform operations.
- Typecasting and conversions
- Example:
```
public class VariablesExample {     
	public static void main(String[] args) {         
		int num1 = 10;         
		int num2 = 5;         
		int sum = num1 + num2;         
		System.out.println("Sum: " + sum);     
	}
}
```

**5. Logic Building with Pattern Programming**

- Use loops (for, while, do-while) to create various patterns.
- Example:
```
public class PatternExample {
	public static void main(String[] args) {
		for (int i = 1; i <= 5; i++) {
			for (int j = 1; j <= i; j++) {
				System.out.print("* ");
			}             
			System.out.println();         
		}    
	} 
}
```
**6. Control Flow Statements**

- Use if-else and switch statements for decision-making.
- Loops (while, do-while, for) for repetitive tasks.
- Break and continue statements
- Example:
```
public class ControlFlowExample {
	public static void main(String[] args) {
		int age = 25;         
		if (age >= 18) {
			System.out.println("You are an adult.");         } 
		else {
			System.out.println("You are a minor.");
		}     
	}
}
```

**7. Arrays, Strings, and Collections**

- Arrays store multiple values of the same type.
- Strings are sequences of characters, and Java provides several String methods.
- Collections like ArrayList, HashSet, and HashMap store and manipulate groups of objects.
- Example:
```
public class ArraysAndStringsExample {
	public static void main(String[] args) {
		int[] numbers = {1, 2, 3, 4, 5};
		String message = "Hello, Java!";
		System.out.println(numbers[2]); // Output: 3
		System.out.println(message.length()); // Output: 12     
	}
}
```

**8. Methods and Classes**

- Methods are blocks of code that perform specific tasks.
- Classes define objects with attributes and behaviours.
- Example:
```
public class MathOperations {   
	public static int add(int a, int b) {
	         return a + b;
	}
}
```
**9. Exception Handling**

- Handle errors and exceptions using try-catch blocks.
- Example:
```
public class ExceptionHandlingExample {
	public static void main(String[] args) {
		try {
			int result = divide(10, 0);
			System.out.println("Result: " + result);         
		} catch (ArithmeticException e) {
			 System.out.println("Error: " + e.getMessage());
		}
	}
	
	public static int divide(int a, int b) {
		return a / b;     
	} 
}
```