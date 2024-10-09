# Part II: Structure

**Structural Design Patterns** deal with the composition of objects and classes to form larger structures while keeping the system flexible and efficient. They help ensure that relationships between entities are easy to manage and understand, improving the design by ensuring that objects and classes are structured in a way that simplifies their interaction.

Here are the key **Structural Design Patterns**:

### 1. **Adapter Pattern (Wrapper)**
   - **Purpose**: Allows incompatible interfaces to work together by wrapping an object and exposing a compatible interface.
   - **When to use**: When you have an existing class with an incompatible interface and need to adapt it to work with other classes.
   - **Example**:
     ```java
     interface MediaPlayer {
         void play(String audioType, String fileName);
     }

     class Mp3Player implements MediaPlayer {
         public void play(String audioType, String fileName) {
             System.out.println("Playing mp3 file: " + fileName);
         }
     }

     class MediaAdapter implements MediaPlayer {
         AdvancedMediaPlayer advancedMediaPlayer;

         public MediaAdapter(String audioType) {
             if (audioType.equalsIgnoreCase("vlc")) {
                 advancedMediaPlayer = new VlcPlayer();
             } else if (audioType.equalsIgnoreCase("mp4")) {
                 advancedMediaPlayer = new Mp4Player();
             }
         }

         public void play(String audioType, String fileName) {
             if (audioType.equalsIgnoreCase("vlc")) {
                 advancedMediaPlayer.playVlc(fileName);
             } else if (audioType.equalsIgnoreCase("mp4")) {
                 advancedMediaPlayer.playMp4(fileName);
             }
         }
     }
     ```

### 2. **Bridge Pattern**
   - **Purpose**: Decouples an abstraction from its implementation so that both can vary independently.
   - **When to use**: When you want to avoid a permanent binding between an abstraction and its implementation and allow either to vary independently.
   - **Example**:
     ```java
     interface Color {
         void applyColor();
     }

     class RedColor implements Color {
         public void applyColor() {
             System.out.println("Applying red color");
         }
     }

     class BlueColor implements Color {
         public void applyColor() {
             System.out.println("Applying blue color");
         }
     }

     abstract class Shape {
         protected Color color;

         public Shape(Color color) {
             this.color = color;
         }

         abstract void draw();
     }

     class Circle extends Shape {
         public Circle(Color color) {
             super(color);
         }

         public void draw() {
             System.out.print("Drawing circle with color ");
             color.applyColor();
         }
     }
     ```

### 3. **Composite Pattern**
   - **Purpose**: Composes objects into tree-like structures to represent part-whole hierarchies. This allows clients to treat individual objects and compositions of objects uniformly.
   - **When to use**: When you need to treat individual objects and compositions of objects uniformly, such as in hierarchical data structures (e.g., a file system).
   - **Example**:
     ```java
     interface Component {
         void showDetails();
     }

     class Leaf implements Component {
         String name;
         public Leaf(String name) { this.name = name; }
         public void showDetails() {
             System.out.println("Leaf: " + name);
         }
     }

     class Composite implements Component {
         List<Component> components = new ArrayList<>();

         public void addComponent(Component component) {
             components.add(component);
         }

         public void showDetails() {
             for (Component component : components) {
                 component.showDetails();
             }
         }
     }
     ```

### 4. **Decorator Pattern**
   - **Purpose**: Adds behavior to objects dynamically by placing them inside a wrapper object that contains this behavior.
   - **When to use**: When you need to add responsibilities to objects dynamically and transparently, without affecting other objects.
   - **Example**:
     ```java
     interface Coffee {
         String getDescription();
         double getCost();
     }

     class SimpleCoffee implements Coffee {
         public String getDescription() { return "Simple coffee"; }
         public double getCost() { return 5.00; }
     }

     class MilkDecorator implements Coffee {
         private Coffee coffee;
         public MilkDecorator(Coffee coffee) {
             this.coffee = coffee;
         }

         public String getDescription() {
             return coffee.getDescription() + ", milk";
         }

         public double getCost() {
             return coffee.getCost() + 1.50;
         }
     }
     ```

### 5. **Facade Pattern**
   - **Purpose**: Provides a simplified interface to a complex subsystem, making it easier for clients to interact with the system.
   - **When to use**: When you want to provide a simple interface to a complex system or reduce dependencies on a complex subsystem.
   - **Example**:
     ```java
     class CPU {
         public void start() { System.out.println("CPU started"); }
     }

     class Memory {
         public void load() { System.out.println("Memory loaded"); }
     }

     class HardDrive {
         public void read() { System.out.println("Hard Drive read"); }
     }

     class ComputerFacade {
         private CPU cpu;
         private Memory memory;
         private HardDrive hardDrive;

         public ComputerFacade() {
             cpu = new CPU();
             memory = new Memory();
             hardDrive = new HardDrive();
         }

         public void startComputer() {
             cpu.start();
             memory.load();
             hardDrive.read();
         }
     }

     // Client
     ComputerFacade computer = new ComputerFacade();
     computer.startComputer();
     ```

### 6. **Flyweight Pattern**
   - **Purpose**: Reduces the cost of creating and using a large number of similar objects by sharing them when possible.
   - **When to use**: When you have a large number of objects that share common state, and you want to reduce memory usage by sharing them.
   - **Example**:
     ```java
     class Tree {
         private String type;
         public Tree(String type) {
             this.type = type;
         }

         public void draw(int x, int y) {
             System.out.println("Drawing tree of type " + type + " at (" + x + ", " + y + ")");
         }
     }

     class TreeFactory {
         private static final Map<String, Tree> treeMap = new HashMap<>();

         public static Tree getTree(String type) {
             Tree tree = treeMap.get(type);
             if (tree == null) {
                 tree = new Tree(type);
                 treeMap.put(type, tree);
             }
             return tree;
         }
     }

     Tree oakTree = TreeFactory.getTree("Oak");
     oakTree.draw(10, 20);
     ```

### 7. **Proxy Pattern**
   - **Purpose**: Provides a surrogate or placeholder for another object to control access to it.
   - **When to use**: When you want to control access to an object, such as lazy initialization, access control, or remote object access.
   - **Example**:
     ```java
     interface Image {
         void display();
     }

     class RealImage implements Image {
         private String fileName;

         public RealImage(String fileName) {
             this.fileName = fileName;
             loadFromDisk();
         }

         private void loadFromDisk() {
             System.out.println("Loading " + fileName);
         }

         public void display() {
             System.out.println("Displaying " + fileName);
         }
     }

     class ProxyImage implements Image {
         private RealImage realImage;
         private String fileName;

         public ProxyImage(String fileName) {
             this.fileName = fileName;
         }

         public void display() {
             if (realImage == null) {
                 realImage = new RealImage(fileName);
             }
             realImage.display();
         }
     }

     // Client
     Image image = new ProxyImage("test.jpg");
     image.display(); // Loading and displaying image
     image.display(); // Displaying image without loading again
     ```

---

### When to Use Which Structural Pattern?

- **Adapter**: When two classes have incompatible interfaces, and you want them to work together without changing the existing code.
- **Bridge**: When you want to separate an abstraction from its implementation so they can vary independently.
- **Composite**: When you need to represent part-whole hierarchies and treat individual objects and groups of objects uniformly.
- **Decorator**: When you want to add behavior to an object dynamically without affecting other objects of the same class.
- **Facade**: When you want to provide a simple interface to a complex subsystem.
- **Flyweight**: When you need to manage a large number of similar objects efficiently by sharing as much data as possible.
- **Proxy**: When you need to control access to an object, such as for performance, security, or resource management reasons.
