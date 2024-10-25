# Preface

The nature of your design is informed by which patterns are present and how they provide contest for each other.

## Qualities
cohesion class=1 resp, methd = 1 func

coupling: ID. Rep. Inh, SubC

No redundance: of Anything ever

Encapsulation: of everything possible

Testability: leverage


---
## Principles

These principles are not strict rules but guidelines that help in designing robust and flexible systems. Many of the **Gang of Four** design patterns, such as Factory, Singleton, and Observer, adhere to these principles to some extent.

Design pattern principles guide the creation and application of design patterns in software development. These principles focus on achieving flexibility, maintainability, and scalability in software systems. Here are the **key principles** of design patterns:

### 1. **Don't Repeat Yourself (DRY)**:
- **Principle**:  Avoid duplication of code and logic. 
- **Explanation**: Every piece of knowledge or functionality should have a single, unambiguous, and authoritative representation in a system. This reduces redundancy, improves maintainability, and avoids inconsistencies.

### 2. **Encapsulate What Varies**
- **Principle**: Identify the aspects of your system that change and separate them from what stays the same.
- **Explanation**: Design your system in a way that allows parts that are subject to change (like algorithms, data structures, or behaviors) to be modified independently without affecting other parts of the system.
- **Example**: In the **Strategy Pattern**, different behaviors (strategies) are encapsulated and can be swapped at runtime without altering the object that uses them.

### 3. **Program to an Interface, Not an Implementation**
- **Principle**: Rely on abstractions (like interfaces or abstract classes) rather than concrete implementations.
- **Explanation**: By depending on interfaces, the code becomes more flexible and allows the substitution of different implementations without changing the client code.
- **Example**: The **Factory Pattern** creates objects based on an interface, enabling the system to instantiate different classes without the client being aware of the specific class being created.

### 4. **Favor Composition Over Inheritance**
- **Principle**: Combine objects dynamically, rather than building rigid hierarchies using inheritance.
- **Explanation**: Composition allows for more flexibility, as behaviors can be added or changed at runtime by combining objects, whereas inheritance can lead to tight coupling and rigidity.
- **Example**: The **Decorator Pattern** uses composition to add responsibilities to objects dynamically, allowing for enhanced flexibility over traditional inheritance.

### 5. **Single Responsibility Principle (SRP)**
- **Principle**: A class should have one, and only one, reason to change.
- **Explanation**: Each class or module should focus on a single task or responsibility, reducing complexity and enhancing maintainability.
- **Example**: A **Repository Pattern** that handles database operations, separating concerns of data access from business logic, adheres to SRP.

### 6. **Open/Closed Principle (OCP)**
- **Principle**: Software entities should be open for extension but closed for modification.
- **Explanation**: Classes or modules should allow for their behavior to be extended (e.g., through inheritance or interfaces) without modifying the existing code. This reduces the risk of introducing bugs into the system.
- **Example**: The **Observer Pattern** allows new observers to be added without modifying the subject, adhering to the open/closed principle.

### 7. **Liskov Substitution Principle (LSP)**
- **Principle**: Subtypes must be substitutable for their base types.
- **Explanation**: Derived classes should be able to replace their base class without altering the correctness of the program. This ensures the consistency and correctness of behavior when polymorphism is used.
- **Example**: In the **Template Method Pattern**, subclasses implement specific steps of an algorithm but can always replace the base class in a manner that preserves functionality.

### 8. **Interface Segregation Principle (ISP)**
- **Principle**: No client should be forced to depend on methods it does not use.
- **Explanation**: It's better to create smaller, specific interfaces rather than a large general-purpose one. This avoids "fat interfaces" and makes the system more modular and adaptable.
- **Example**: In the **Adapter Pattern**, a class can adapt to different interfaces, keeping each interface focused and aligned with the needs of its clients.

### 9. **Dependency Inversion Principle (DIP)**
- **Principle**: High-level modules should not depend on low-level modules. Both should depend on abstractions.
- **Explanation**: Instead of high-level code relying directly on low-level details, both should rely on interfaces or abstractions, creating a flexible and loosely coupled system.
- **Example**: The **Dependency Injection Pattern** adheres to DIP by injecting dependencies (e.g., service objects) into a class from the outside, decoupling high-level logic from specific implementations.

### 10. **Least Knowledge Principle (Law of Demeter)**
- **Principle**: A class should only talk to its immediate "friends" and not to other classes' internal details.
- **Explanation**: Each class or object should interact only with objects closely related to it, avoiding excessive knowledge of other objects. This reduces dependencies and simplifies the system.
- **Example**: The **Facade Pattern** provides a simplified interface to a set of subsystems, adhering to the Least Knowledge Principle by shielding clients from the internal complexity.



---

These principles form the foundation for many **design patterns** (such as Factory, Singleton, Decorator, etc.) and enable developers to create systems that are more **flexible, reusable,** and **maintainable** over time. Following these guidelines helps avoid common pitfalls like tight coupling, rigid design, and code duplication.

---
## Practices
### 1. **State Private**
### 2. **Code Standards**
### 3. **Program by intent**

---
## Wisdom
design to interfaces

favor comp. over inh

enc. conc's that vary

coh. of perspective

---

## Patterns
1. **Singleton**:
2. **Factory**:
3. **Abstract Factory**:
4. **Prototype**:
5. **Builder**:
6. **Bridge**:
7. **Adapter**:
8. **Facade**:
9. **Decorator**:
10. **Composite**:
11. **Flyweight**:
12. **Proxy**:
13. **Strategy**:
14. **Template**:
15. **Command**:
16. **Visitor**:
17. **Iterator**:
18. **Observer**:
19. **Mediator**:
20. **Memento**:
21. **Interpreter**:
22. **State**:
23. **Chain of Responsibility**:

---
##  Paradigm