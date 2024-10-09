# Part I: Creation Design Patterns

**Creation Design Patterns** are a category of software design patterns that deal with object creation mechanisms. Their purpose is to create objects in a manner that is suitable for the situation at hand, without needing the client code to know the details of how objects are constructed. This enhances the flexibility and scalability of the system.

Here are the key **Creational Design Patterns**:

### 1. **Factory Method Pattern**
   - **Purpose**: Define an interface for creating an object, but let subclasses alter the type of objects that will be created.
   - **When to use**: Use when the exact type of object that needs to be created is determined by subclasses.
   - **Example**:
     ```java
     interface Product {
         void create();
     }

     class ConcreteProductA implements Product {
         public void create() {
             System.out.println("Product A created");
         }
     }

     class ConcreteProductB implements Product {
         public void create() {
             System.out.println("Product B created");
         }
     }

     abstract class Creator {
         abstract Product factoryMethod();
     }

     class CreatorA extends Creator {
         Product factoryMethod() {
             return new ConcreteProductA();
         }
     }

     class CreatorB extends Creator {
         Product factoryMethod() {
             return new ConcreteProductB();
         }
     }
     ```

### 2. **Abstract Factory Pattern**
   - **Purpose**: Provides an interface for creating families of related or dependent objects without specifying their concrete classes.
   - **When to use**: When the system needs to be independent of how its objects are created and represented, and the system needs to be configured with one of multiple families of products.
   - **Example**:
     ```java
     interface GUIFactory {
         Button createButton();
         Checkbox createCheckbox();
     }

     class WinFactory implements GUIFactory {
         public Button createButton() { return new WinButton(); }
         public Checkbox createCheckbox() { return new WinCheckbox(); }
     }

     class MacFactory implements GUIFactory {
         public Button createButton() { return new MacButton(); }
         public Checkbox createCheckbox() { return new MacCheckbox(); }
     }
     ```

### 3. **Builder Pattern**
   - **Purpose**: Separate the construction of a complex object from its representation, allowing the same construction process to create different representations.
   - **When to use**: When you need to build an object that requires multiple steps or when the construction process is complex and involves several options.
   - **Example**:
     ```java
     class House {
         private String foundation;
         private String structure;
         private String roof;

         // Getters and setters omitted for brevity
     }

     class HouseBuilder {
         private House house;

         public HouseBuilder() { house = new House(); }
         public HouseBuilder buildFoundation(String foundation) {
             house.setFoundation(foundation);
             return this;
         }
         public HouseBuilder buildStructure(String structure) {
             house.setStructure(structure);
             return this;
         }
         public HouseBuilder buildRoof(String roof) {
             house.setRoof(roof);
             return this;
         }
         public House build() {
             return house;
         }
     }

     House house = new HouseBuilder()
                         .buildFoundation("Concrete")
                         .buildStructure("Wood")
                         .buildRoof("Shingles")
                         .build();
     ```

### 4. **Prototype Pattern**
   - **Purpose**: Create new objects by copying an existing object, known as the prototype. This pattern helps avoid the cost of creating objects from scratch.
   - **When to use**: When the process of creating an object is costly or complex and you want to avoid creating new instances by cloning existing ones.
   - **Example**:
     ```java
     class Shape implements Cloneable {
         String type;
         
         public Shape(String type) {
             this.type = type;
         }

         public Shape clone() throws CloneNotSupportedException {
             return (Shape) super.clone();
         }
     }

     Shape original = new Shape("Circle");
     Shape clone = original.clone();
     ```

### 5. **Singleton Pattern**
   - **Purpose**: Ensures that a class has only one instance and provides a global point of access to it.
   - **When to use**: When only one instance of a class is needed throughout the system, such as managing shared resources (e.g., database connections).
   - **Example**:
     ```java
     class Singleton {
         private static Singleton instance;

         private Singleton() { }

         public static Singleton getInstance() {
             if (instance == null) {
                 instance = new Singleton();
             }
             return instance;
         }
     }

     Singleton singleton = Singleton.getInstance();
     ```

---

### When to Use Which Creational Pattern?

- **Factory Method**: When you have a superclass that defines the general behavior, but subclasses should determine which concrete class to instantiate.
- **Abstract Factory**: When you need to create families of related objects and want to ensure the objects are used together.
- **Builder**: When the object creation process is complex or involves multiple optional parameters.
- **Prototype**: When creating a new instance of an object is expensive, or you need to create multiple copies of an object that has a defined state.
- **Singleton**: When exactly one instance of a class is required and you want to control its global access.



