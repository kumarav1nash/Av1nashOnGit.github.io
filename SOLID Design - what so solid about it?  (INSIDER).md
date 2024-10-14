The SOLID principles in object-oriented programming form the foundation for writing clean, maintainable, and scalable code. 

Applied Correctly will help us as a developer to write better software design, reduced complexity and more flexibility.

Let’s break down each principle with detailed explanations and examples using Java / Spring Boot.

1. Single Responsibility Principle (SRP)
**Definition:** A class should have only one reason to change, meaning it should have only one job or responsibility. In Spring boot context if your service is doing multiple things oh boy you're making blunder, here's an example

**Violating SRP**
```
public class UserService {
    public void createUser(User user) {
        // Business logic to create a user
    }
    
    public void validateUser(User user) {
        // Validation logic
    }
    
    public void sendWelcomeEmail(User user) {
        // Email sending logic
    }
}
```

Whats wrong in the above example can you make a guess here.
Here **UserService** is handling both user creation and email notification, violating SRP

**Solution**: Break Down The Logic into Separate classes with their own logic
```
@Service
public class UserService {
    public void createUser(User user) {
        // Business logic to create a user
    }
}

@Service
public class EmailService {
    public void sendWelcomeEmail(User user) {
        // Email sending logic
    }
}
```

2. Open/Closed Principle (OCP)
**Definition:** A class should be open for extension but closed for modification. It encourages the use of inheritance and polymorphism to extend functionality without changing existing code.


**Example in Spring Boot:** Suppose you have a `PaymentService` that processes various types of payments. Instead of modifying the service every time a new payment method is added, you can extend it.

Violating OCP
```
public class PaymentService {
    public void processPayment(String type) {
        if (type.equals("credit")) {
            // Process credit payment
        } else if (type.equals("paypal")) {
            // Process PayPal payment
        }
    }
}
```

This requires modification every time a new payment method is added. **BAD IDEA**

**Solution:** Use interfaces or abstract classes to extend functionality without modifying the original class.
```
public interface PaymentMethod {
    void process();
}

public class CreditPayment implements PaymentMethod {
    @Override
    public void process() {
        // Process credit payment
    }
}

public class PaypalPayment implements PaymentMethod {
    @Override
    public void process() {
        // Process PayPal payment
    }
}

@Service
public class PaymentService {
    public void processPayment(PaymentMethod method) {
        method.process();
    }
}
```

Now, new payment methods can be added without modifying the existing `PaymentService`.

3. Liskov Substitution Principle (LSP)

**Definition:** Subtypes must be substitutable for their base types without affecting the correctness of the program.

**Example in Spring Boot:** When creating a class hierarchy, ensure that subclasses can stand in for their base classes without breaking the application.

**Violating LSP**
```
public class Bird {
    public void fly() {
        // All birds can fly
    }
}

public class Ostrich extends Bird {
    @Override
    public void fly() {
        throw new UnsupportedOperationException("Ostrich can't fly");
    }
}
```

This violates LSP, as `Ostrich` can't replace `Bird` without altering behavior.

**Solution:** Redesign the hierarchy to avoid violating LSP.
```
public abstract class Bird {
    public abstract void move();
}

public class FlyingBird extends Bird {
    @Override
    public void move() {
        // Fly logic
    }
}

public class Ostrich extends Bird {
    @Override
    public void move() {
        // Ostrich walk logic
    }
}

```

Now `FlyingBird` and `Ostrich` can substitute `Bird` without breaking the functionality.

4. Interface Segregation Principle (ISP)
**Definition:** Clients should not be forced to depend on methods they do not use. Large interfaces should be split into smaller, more specific ones.

**Example in Spring Boot:** Suppose you have an interface with multiple unrelated methods.

**Violating ISP**
```
public interface Worker {
    void work();
    void eat();
    void sleep();
}
```

Now every class implementing `Worker` must provide implementations for `eat()` and `sleep()`, even if not required.

**Solution:** Separate interfaces based on their specific needs.
```
public interface Workable {
    void work();
}

public interface Eatable {
    void eat();
}

public class Employee implements Workable, Eatable {
    @Override
    public void work() {
        // Work logic
    }

    @Override
    public void eat() {
        // Eat logic
    }
}
//Now You know why Employee can not sleep XD

```

Now, classes only implement methods relevant to their roles.

5. Dependency Inversion Principle (DIP)
**Definition:** High-level modules should not depend on low-level modules. Both should depend on abstractions. Additionally, abstractions should not depend on details; details should depend on abstractions.

**Example in Spring Boot:** In a typical Spring Boot application, dependency injection is widely used to adhere to DIP.

**Violating DIP**
```
public class UserService {
    private EmailService emailService = new EmailService();

    public void sendNotification() {
        emailService.sendEmail();
    }
}
```

Here, `UserService` directly depends on `EmailService`. Any change in `EmailService` would require changes in `UserService`.

**Solution:** Inject `EmailService` through an interface and use Spring's dependency injection to provide the implementation.

```
public interface NotificationService {
    void notifyUser();
}

@Service
public class EmailService implements NotificationService {
    @Override
    public void notifyUser() {
        // Email sending logic
    }
}

@Service
public class UserService {
    private final NotificationService notificationService;

    @Autowired
    public UserService(NotificationService notificationService) {
        this.notificationService = notificationService;
    }

    public void sendNotification() {
        notificationService.notifyUser();
    }
}
```

Now, `UserService` depends on an abstraction (`NotificationService`) and not a concrete implementation.


### Conclusion

Adhering to the **SOLID principles** in Java Spring Boot applications results in more maintainable, flexible, and scalable code. These principles are crucial for software development at scale and ensure that your application can easily accommodate new features and changes without causing major disruptions.

Each principle in the SOLID framework plays a vital role in achieving modularity and reducing tight coupling between components, leading to better code quality.

