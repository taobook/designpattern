# Preface

## Practices
### 1. **State Private**
### 2. **Code Standards**
### 3. **Program by intent**

---

## Principals

These principles are not strict rules but guidelines that help in designing robust and flexible systems. Many of the **Gang of Four** design patterns, such as Factory, Singleton, and Observer, adhere to these principles to some extent.

Design pattern principles guide the creation and application of design patterns in software development. These principles focus on achieving flexibility, maintainability, and scalability in software systems. Here are the **key principles** of design patterns:

### 1. **Encapsulate What Varies**
- **Principle**: Identify the aspects of your system that change and separate them from what stays the same.
- **Explanation**: Design your system in a way that allows parts that are subject to change (like algorithms, data structures, or behaviors) to be modified independently without affecting other parts of the system.
- **Example**: In the **Strategy Pattern**, different behaviors (strategies) are encapsulated and can be swapped at runtime without altering the object that uses them.

### 2. **Program to an Interface, Not an Implementation**
- **Principle**: Rely on abstractions (like interfaces or abstract classes) rather than concrete implementations.
- **Explanation**: By depending on interfaces, the code becomes more flexible and allows the substitution of different implementations without changing the client code.
- **Example**: The **Factory Pattern** creates objects based on an interface, enabling the system to instantiate different classes without the client being aware of the specific class being created.

### 3. **Favor Composition Over Inheritance**
> Favor **object composition over class inheritance** when reusing functionality. Instead of creating rigid hierarchies, functionality can be composed using objects and interfaces, providing more flexibility and reducing the complexity of inheritance chains.
- **Principle**: Combine objects dynamically, rather than building rigid hierarchies using inheritance.
- **Explanation**: Composition allows for more flexibility, as behaviors can be added or changed at runtime by combining objects, whereas inheritance can lead to tight coupling and rigidity.
- **Example**: The **Decorator Pattern** uses composition to add responsibilities to objects dynamically, allowing for enhanced flexibility over traditional inheritance.

### 4. **Single Responsibility Principle (SRP)**
> A class or module should have **one and only one reason to change**, meaning it should only have one responsibility or function. This reduces complexity and makes the system easier to maintain and evolve.
- **Principle**: A class should have one, and only one, reason to change.
- **Explanation**: Each class or module should focus on a single task or responsibility, reducing complexity and enhancing maintainability.
- **Example**: A **Repository Pattern** that handles database operations, separating concerns of data access from business logic, adheres to SRP.

### 5. **Open/Closed Principle (OCP)**
> Software entities (classes, modules, functions) should be **open for extension but closed for modification**. This means you should be able to add new functionality without changing existing code, which helps in minimizing bugs or side effects.
- **Principle**: Software entities should be open for extension but closed for modification.
- **Explanation**: Classes or modules should allow for their behavior to be extended (e.g., through inheritance or interfaces) without modifying the existing code. This reduces the risk of introducing bugs into the system.
- **Example**: The **Observer Pattern** allows new observers to be added without modifying the subject, adhering to the open/closed principle.

### 6. **Liskov Substitution Principle (LSP)**
> Objects of a **derived class must be replaceable for objects of the base class** without affecting the correctness of the program. This ensures that subclasses can stand in for their parent classes without altering the behavior of the code.
- **Principle**: Subtypes must be substitutable for their base types.
- **Explanation**: Derived classes should be able to replace their base class without altering the correctness of the program. This ensures the consistency and correctness of behavior when polymorphism is used.
- **Example**: In the **Template Method Pattern**, subclasses implement specific steps of an algorithm but can always replace the base class in a manner that preserves functionality.

### 7. **Interface Segregation Principle (ISP)**
> Clients should not be forced to depend on interfaces they do not use. Instead, **multiple specific interfaces** are better than a single general-purpose one. This avoids "fat" interfaces and ensures that clients are only exposed to methods that are relevant to them.
- **Principle**: No client should be forced to depend on methods it does not use.
- **Explanation**: It's better to create smaller, specific interfaces rather than a large general-purpose one. This avoids "fat interfaces" and makes the system more modular and adaptable.
- **Example**: In the **Adapter Pattern**, a class can adapt to different interfaces, keeping each interface focused and aligned with the needs of its clients.

### 8. **Dependency Inversion Principle (DIP)**
> High-level modules should not depend on low-level modules. Both should depend on **abstractions** (e.g., interfaces), not on concrete implementations. This encourages loose coupling and makes the system more flexible and testable.
- **Principle**: High-level modules should not depend on low-level modules. Both should depend on abstractions.
- **Explanation**: Instead of high-level code relying directly on low-level details, both should rely on interfaces or abstractions, creating a flexible and loosely coupled system.
- **Example**: The **Dependency Injection Pattern** adheres to DIP by injecting dependencies (e.g., service objects) into a class from the outside, decoupling high-level logic from specific implementations.

### 9. **Least Knowledge Principle (Law of Demeter)**
- **Principle**: A class should only talk to its immediate "friends" and not to other classes' internal details.
- **Explanation**: Each class or object should interact only with objects closely related to it, avoiding excessive knowledge of other objects. This reduces dependencies and simplifies the system.
- **Example**: The **Facade Pattern** provides a simplified interface to a set of subsystems, adhering to the Least Knowledge Principle by shielding clients from the internal complexity.

### 10. **Don't Repeat Yourself (DRY)**:
> **Avoid duplication** of code and logic. Every piece of knowledge or functionality should have a single, unambiguous, and authoritative representation in a system. This reduces redundancy, improves maintainability, and avoids inconsistencies.

---

These principles form the foundation for many **design patterns** (such as Factory, Singleton, Decorator, etc.) and enable developers to create systems that are more **flexible, reusable,** and **maintainable** over time. Following these guidelines helps avoid common pitfalls like tight coupling, rigid design, and code duplication.

---

## Patterns
### 1. **Singleton**:
---
