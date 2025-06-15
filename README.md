# Spring Boot IoC, Annotations, Beans, and Application Context Example

## Overview

This project demonstrates the core concepts of the Spring Framework:
- **Inversion of Control (IoC)**
- **Annotations**
- **Beans**
- **Application Context**

It provides simple examples of how these concepts work together to create a loosely-coupled, easily testable Java application.

---

## Key Concepts

### 1. Inversion of Control (IoC)

**IoC** is a design principle where the control of object creation and dependency management is transferred from the program itself to a container or framework (in this case, Spring). This makes your code more modular and easier to maintain.

**Example:**  
Instead of creating objects with `new`, you let Spring create and manage them for you.

---

### 2. Beans

A **bean** is any object that is managed by the Spring IoC container. Beans are defined in configuration files (like `applicationContext.xml`) or via annotations in your code.

**Example:**  
A `UserService` or `OrderService` class can be a bean.

---

### 3. Annotations

**Annotations** are special markers in Java (like `@Service`, `@Autowired`, `@Component`) that tell Spring how to manage your classes and their dependencies.

- `@Component` – Marks a class as a Spring bean.
- `@Service` – Specialization of `@Component` for service classes.
- `@Autowired` – Tells Spring to automatically inject dependencies.

---

### 4. Application Context

The **Application Context** is the central interface in Spring for providing configuration information to the application. It manages the lifecycle of beans and handles dependency injection.

---

## Project Structure

```
app/
├── src/
│   └── main/
│       ├── groovy/
│       │   └── org/
│       │       └── example/
│       │           ├── App.groovy
│       │           ├── services/
│       │           │   ├── UserService.java
│       │           │   └── OrderService.java
│       │           └── bean/
│       │               └── UserConfig.java
│       └── resources/
│           └── applicationContext.xml
```

- **App.groovy**: Main entry point, starts the Spring application.
- **UserService.java**: Service bean for user operations.
- **OrderService.java**: Service bean for order operations.
- **UserConfig.java**: Configuration bean for user settings.
- **applicationContext.xml**: XML configuration for beans and dependencies.

---

## How It Works

1. **Beans are defined** in `applicationContext.xml` or via annotations.
2. **Spring creates and manages** these beans when the application starts.
3. **Dependencies are injected** automatically (using `@Autowired` or XML).
4. **Business logic** is executed using these managed beans.

---

## Example: Defining and Using Beans

**applicationContext.xml**
```xml
<bean id="userService" class="org.example.services.UserService"/>
<bean id="orderService" class="org.example.services.OrderService">
    <constructor-arg ref="userService"/>
</bean>
```

**UserService.java**
```java
@Service
public class UserService {
    // User-related logic
}
```

**OrderService.java**
```java
@Service
public class OrderService {
    private final UserService userService;

    @Autowired
    public OrderService(UserService userService) {
        this.userService = userService;
    }
}
```

---

## Running the Project

1. **Build the project** using your preferred IDE or with Maven/Gradle.
2. **Run `App.groovy`** or the main class to start the application.
3. **Spring will automatically create and wire beans** as defined in the configuration.

---

## Why Use IoC and Beans?

- **Loose Coupling:** Classes don’t need to know how to create their dependencies.
- **Easier Testing:** You can easily swap out beans for mocks in tests.
- **Centralized Configuration:** All dependencies are managed in one place.

---

## Further Reading

- [Spring Framework Documentation](https://docs.spring.io/spring-framework/docs/current/reference/html/core.html)
- [Spring Boot Reference Guide](https://docs.spring.io/spring-boot/docs/current/reference/html/)

---

**This project is a simple, practical demonstration of how Spring’s IoC container, beans, annotations, and application context work together to build robust Java applications.**
