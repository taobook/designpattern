# Part III: Behavior

**Behavioral Design Patterns** focus on communication and interaction between objects. They help define the way objects interact with each other, ensuring that the system is flexible, reusable, and easy to maintain.

Here are the key **Behavioral Design Patterns**:

### 1. **Chain of Responsibility Pattern**
   - **Purpose**: Allows a request to be passed along a chain of handlers. Each handler decides whether to process the request or pass it to the next handler in the chain.
   - **When to use**: When multiple objects can handle a request, but the handler is determined at runtime.
   - **Example**:
     ```java
     abstract class Logger {
         public static int INFO = 1;
         public static int DEBUG = 2;
         public static int ERROR = 3;
         protected int level;
         protected Logger nextLogger;

         public void setNextLogger(Logger nextLogger) {
             this.nextLogger = nextLogger;
         }

         public void logMessage(int level, String message) {
             if (this.level <= level) {
                 write(message);
             }
             if (nextLogger != null) {
                 nextLogger.logMessage(level, message);
             }
         }

         abstract protected void write(String message);
     }

     class ConsoleLogger extends Logger {
         public ConsoleLogger(int level) {
             this.level = level;
         }

         @Override
         protected void write(String message) {
             System.out.println("Console::Logger: " + message);
         }
     }

     class ErrorLogger extends Logger {
         public ErrorLogger(int level) {
             this.level = level;
         }

         @Override
         protected void write(String message) {
             System.out.println("Error::Logger: " + message);
         }
     }

     Logger loggerChain = getChainOfLoggers();
     loggerChain.logMessage(Logger.ERROR, "This is an error message.");
     ```

### 2. **Command Pattern**
   - **Purpose**: Encapsulates a request as an object, thereby allowing users to parameterize clients with queues, requests, and operations.
   - **When to use**: When you want to issue requests as objects, allowing for queueing, logging, undo/redo operations.
   - **Example**:
     ```java
     interface Command {
         void execute();
     }

     class Light {
         public void on() { System.out.println("Light is on"); }
         public void off() { System.out.println("Light is off"); }
     }

     class LightOnCommand implements Command {
         private Light light;

         public LightOnCommand(Light light) {
             this.light = light;
         }

         public void execute() {
             light.on();
         }
     }

     class RemoteControl {
         private Command command;

         public void setCommand(Command command) {
             this.command = command;
         }

         public void pressButton() {
             command.execute();
         }
     }

     Light light = new Light();
     Command lightOn = new LightOnCommand(light);
     RemoteControl remote = new RemoteControl();
     remote.setCommand(lightOn);
     remote.pressButton();
     ```

### 3. **Interpreter Pattern**
   - **Purpose**: Defines a grammatical representation for a language and an interpreter to interpret sentences in that language.
   - **When to use**: When you need to interpret expressions defined in a formal language.
   - **Example**:
     ```java
     interface Expression {
         boolean interpret(String context);
     }

     class TerminalExpression implements Expression {
         private String data;

         public TerminalExpression(String data) {
             this.data = data;
         }

         public boolean interpret(String context) {
             return context.contains(data);
         }
     }

     Expression isMale = new TerminalExpression("John");
     System.out.println("John is male? " + isMale.interpret("John"));
     ```

### 4. **Iterator Pattern**
   - **Purpose**: Provides a way to access the elements of an aggregate object sequentially without exposing its underlying structure.
   - **When to use**: When you need to traverse a collection without exposing its internal representation.
   - **Example**:
     ```java
     interface Iterator {
         boolean hasNext();
         Object next();
     }

     interface Container {
         Iterator getIterator();
     }

     class NameRepository implements Container {
         public String[] names = { "John", "Jane", "Michael" };

         public Iterator getIterator() {
             return new NameIterator();
         }

         private class NameIterator implements Iterator {
             int index;

             public boolean hasNext() {
                 return index < names.length;
             }

             public Object next() {
                 if (this.hasNext()) {
                     return names[index++];
                 }
                 return null;
             }
         }
     }

     NameRepository namesRepository = new NameRepository();
     for (Iterator iter = namesRepository.getIterator(); iter.hasNext();) {
         System.out.println("Name: " + iter.next());
     }
     ```

### 5. **Mediator Pattern**
   - **Purpose**: Defines an object that controls how a set of objects interact, reducing dependencies between them.
   - **When to use**: When you have multiple objects interacting in complex ways and want to avoid direct coupling between them.
   - **Example**:
     ```java
     interface Mediator {
         void sendMessage(String message, Colleague colleague);
     }

     abstract class Colleague {
         protected Mediator mediator;

         public Colleague(Mediator mediator) {
             this.mediator = mediator;
         }
     }

     class User extends Colleague {
         public User(Mediator mediator) {
             super(mediator);
         }

         public void send(String message) {
             System.out.println("Sending message: " + message);
             mediator.sendMessage(message, this);
         }

         public void receive(String message) {
             System.out.println("Received message: " + message);
         }
     }

     class ChatMediator implements Mediator {
         private List<User> users = new ArrayList<>();

         public void addUser(User user) {
             users.add(user);
         }

         public void sendMessage(String message, Colleague colleague) {
             for (User user : users) {
                 if (user != colleague) {
                     user.receive(message);
                 }
             }
         }
     }

     ChatMediator mediator = new ChatMediator();
     User user1 = new User(mediator);
     User user2 = new User(mediator);
     mediator.addUser(user1);
     mediator.addUser(user2);
     user1.send("Hello everyone!");
     ```

### 6. **Memento Pattern**
   - **Purpose**: Captures and externalizes an object's internal state without violating encapsulation, allowing the object to be restored to this state later.
   - **When to use**: When you need to save an object's state so it can be restored later (undo functionality).
   - **Example**:
     ```java
     class Memento {
         private String state;

         public Memento(String state) {
             this.state = state;
         }

         public String getState() {
             return state;
         }
     }

     class Originator {
         private String state;

         public void setState(String state) {
             this.state = state;
         }

         public Memento saveStateToMemento() {
             return new Memento(state);
         }

         public void getStateFromMemento(Memento memento) {
             state = memento.getState();
         }
     }

     Originator originator = new Originator();
     originator.setState("State1");
     Memento memento = originator.saveStateToMemento();
     originator.setState("State2");
     originator.getStateFromMemento(memento);
     ```

### 7. **Observer Pattern**
   - **Purpose**: Defines a one-to-many dependency between objects, so that when one object changes state, all its dependents are notified and updated automatically.
   - **When to use**: When you need to notify multiple objects about the state changes of another object.
   - **Example**:
     ```java
     interface Observer {
         void update();
     }

     class Subject {
         private List<Observer> observers = new ArrayList<>();
         private int state;

         public int getState() {
             return state;
         }

         public void setState(int state) {
             this.state = state;
             notifyAllObservers();
         }

         public void attach(Observer observer) {
             observers.add(observer);
         }

         private void notifyAllObservers() {
             for (Observer observer : observers) {
                 observer.update();
             }
         }
     }

     class ConcreteObserver implements Observer {
         private Subject subject;

         public ConcreteObserver(Subject subject) {
             this.subject = subject;
         }

         public void update() {
             System.out.println("Observer state: " + subject.getState());
         }
     }

     Subject subject = new Subject();
     Observer observer = new ConcreteObserver(subject);
     subject.attach(observer);
     subject.setState(10);
     ```

### 8. **State Pattern**
   - **Purpose**: Allows an object to change its behavior when its internal state changes. The object will appear to change its class.
   - **When to use**: When an object's behavior depends on its state, and it must change behavior dynamically at runtime.
    The **State Pattern** is a behavioral design pattern that allows an object to change its behavior when its internal state changes. It encapsulates state-specific behavior into separate classes, making the object appear to change its class when its state changes.
    
    ### **Purpose**
    - The State pattern allows an object to alter its behavior when its internal state changes, by delegating state-specific behavior to different state objects.
    - It helps avoid large conditional statements (like `if-else` or `switch`) for state transitions.
    
    ### **When to Use the State Pattern**
    - When an object's behavior depends on its state and it must change its behavior at runtime depending on its internal state.
    - When you have a lot of conditionals or `if-else` statements that depend on the state of an object.
      
    ### **Key Components**
    1. **Context**: This is the class that maintains an instance of one of the state classes. It delegates state-specific behavior to the current state object.
    2. **State Interface**: Declares the state-specific behaviors that concrete state classes must implement.
    3. **Concrete State Classes**: Implement the behavior associated with a particular state of the context.
    
    ### **Example: Traffic Light System**
    
    Let's consider a traffic light system where the light can be in a "Green", "Yellow", or "Red" state, and each state has its own behavior.
    
    #### **Code Example**
    
    ```java
    // 1. State Interface
    interface TrafficLightState {
        void handleRequest(TrafficLightContext context);
    }
    
    // 2. Concrete State Classes
    class GreenLightState implements TrafficLightState {
        @Override
        public void handleRequest(TrafficLightContext context) {
            System.out.println("Green Light: Cars can go.");
            context.setState(new YellowLightState()); // Change to Yellow
        }
    }
    
    class YellowLightState implements TrafficLightState {
        @Override
        public void handleRequest(TrafficLightContext context) {
            System.out.println("Yellow Light: Prepare to stop.");
            context.setState(new RedLightState()); // Change to Red
        }
    }
    
    class RedLightState implements TrafficLightState {
        @Override
        public void handleRequest(TrafficLightContext context) {
            System.out.println("Red Light: Cars must stop.");
            context.setState(new GreenLightState()); // Change to Green
        }
    }
    
    // 3. Context Class
    class TrafficLightContext {
        private TrafficLightState state;
    
        public TrafficLightContext() {
            // Start with Green light by default
            state = new GreenLightState();
        }
    
        public void setState(TrafficLightState state) {
            this.state = state;
        }
    
        public void request() {
            state.handleRequest(this);
        }
    }
    
    // Client
    public class TrafficLightSystem {
        public static void main(String[] args) {
            TrafficLightContext trafficLight = new TrafficLightContext();
    
            // Cycle through states
            trafficLight.request();  // Green Light -> Yellow
            trafficLight.request();  // Yellow Light -> Red
            trafficLight.request();  // Red Light -> Green
        }
    }
    ```
    
    ### **Explanation**
    - **Context (`TrafficLightContext`)**: It maintains the current state of the traffic light and delegates the behavior to the current state object. It starts with the `GreenLightState` by default.
    - **State Interface (`TrafficLightState`)**: Declares a method `handleRequest()` that each state must implement.
    - **Concrete State Classes (`GreenLightState`, `YellowLightState`, `RedLightState`)**: Each state class defines the behavior corresponding to a specific traffic light state.
    - **Transition**: The state changes as each state's behavior is invoked. When `trafficLight.request()` is called, the current state’s behavior is executed, and the state transitions to the next one (Green → Yellow → Red → Green).
    
    ### **Advantages of State Pattern**
    - **Simplifies conditional logic**: Avoids large, complex conditional statements (e.g., `if-else` or `switch`) by delegating state-specific behavior to different state classes.
    - **Extensibility**: New states can be added without changing existing code.
    - **Separation of concerns**: Each state is encapsulated in its own class, making the code cleaner and easier to maintain.
    
    ### **When Not to Use the State Pattern**
    - If there are only a few states, the overhead of creating separate state classes may not be justified.
    - If state changes do not involve complex behavior or if they can be managed with simple conditionals, the State pattern might be overkill.
    
    ### **Real-World Use Cases**
    - **Game development**: Managing the state of a character (e.g., walking, running, jumping).
    - **UI workflows**: Different states of a UI component (e.g., enabled, disabled, loading).
    - **Network connections**: Managing network states (e.g., connected, disconnected, reconnecting).

Behavioral Design Patterns focus on improving communication between objects and enhancing flexibility in the assignment of responsibilities. These patterns help define how objects interact and communicate, allowing the system to be more flexible, scalable, and maintainable.

Here is a summary of **Behavioral Design Patterns**:

### 1. **Chain of Responsibility Pattern**
   - **Purpose**: Allows a request to be passed along a chain of handlers. Each handler decides whether to process the request or pass it to the next handler.
   - **Use case**: Logging systems with different levels (info, debug, error) where each level is handled by a different logger.
   - **Example**: An ATM machine that dispenses money through different handlers (50s, 20s, 10s).

### 2. **Command Pattern**
   - **Purpose**: Encapsulates a request as an object, allowing you to parameterize clients with queues, requests, and operations. It also supports undo/redo operations.
   - **Use case**: A GUI with buttons like "Cut", "Copy", "Paste", where each button click is handled as a command object.
   - **Example**: Remote controls or text editors with undo/redo functionality.

### 3. **Interpreter Pattern**
   - **Purpose**: Defines a grammatical representation for a language and an interpreter to interpret sentences in that language.
   - **Use case**: When you need to interpret expressions, such as in parsing mathematical expressions or programming languages.
   - **Example**: SQL query interpreters, regular expression interpreters.

### 4. **Iterator Pattern**
   - **Purpose**: Provides a way to access the elements of a collection object sequentially without exposing its underlying structure.
   - **Use case**: Iterating over a collection of items (lists, trees, graphs) without exposing the internal details.
   - **Example**: A file directory iterator that processes files in a folder one by one.

### 5. **Mediator Pattern**
   - **Purpose**: Defines an object that coordinates interactions between other objects, reducing dependencies between them.
   - **Use case**: Chat rooms where users interact via a central server (mediator), reducing direct dependencies between users.
   - **Example**: An air traffic control system that manages communication between airplanes.

### 6. **Memento Pattern**
   - **Purpose**: Captures an object's internal state without violating encapsulation, so that the object can be restored to this state later (undo functionality).
   - **Use case**: Text editors where you can undo or redo changes.
   - **Example**: Game saves where the player can restore the game state from a previous point.

### 7. **Observer Pattern**
   - **Purpose**: Defines a one-to-many relationship between objects so that when one object changes state, all its dependents are notified automatically.
   - **Use case**: Event-driven systems like GUIs where a button click updates multiple listeners or observers.
   - **Example**: A news agency where changes in news articles are automatically pushed to subscribers.

### 8. **State Pattern**
   - **Purpose**: Allows an object to change its behavior when its internal state changes, making it appear as if the object has changed its class.
   - **Use case**: Vending machines or traffic lights where the behavior changes based on the current state (idle, processing, dispensing).
   - **Example**: A document in a text editor that transitions between "Draft", "Review", and "Published" states.

### 9. **Strategy Pattern**
   - **Purpose**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable. The strategy pattern allows the algorithm to vary independently from the clients that use it.
   - **Use case**: Different sorting algorithms (quick sort, merge sort, bubble sort) where the algorithm can be chosen at runtime.
   - **Example**: Payment methods in an e-commerce system where users can switch between strategies like "Credit Card", "PayPal", "Cryptocurrency".

### 10. **Template Method Pattern**
   - **Purpose**: Defines the skeleton of an algorithm in a method, deferring some steps to subclasses. Subclasses can redefine certain steps without changing the algorithm's structure.
   - **Use case**: Frameworks where the general workflow is fixed, but individual steps can be customized.
   - **Example**: A cooking recipe where the steps are fixed but specific ingredients or methods can vary.

### 11. **Visitor Pattern**
   - **Purpose**: Separates an algorithm from the object structure on which it operates. The Visitor pattern allows you to add new operations to a class hierarchy without changing the classes.
   - **Use case**: Object structures that rarely change but need new operations added frequently (e.g., compilers processing different types of nodes in an abstract syntax tree).
   - **Example**: A file system where visitors perform different operations (compression, virus scan) on files and directories.

---

### Detailed Example: **Observer Pattern**
The Observer Pattern allows an object (subject) to notify multiple dependent objects (observers) about changes in its state without coupling the subject to the observers.

#### Example: Stock Market Price Update

```java
// Observer interface
interface Observer {
    void update(float price);
}

// Concrete observer classes
class Investor implements Observer {
    private String name;

    public Investor(String name) {
        this.name = name;
    }

    @Override
    public void update(float price) {
        System.out.println(name + " has been notified of new stock price: $" + price);
    }
}

// Subject interface
interface Stock {
    void addObserver(Observer observer);
    void removeObserver(Observer observer);
    void notifyObservers();
}

// Concrete subject class
class GoogleStock implements Stock {
    private List<Observer> observers = new ArrayList<>();
    private float price;

    public void setPrice(float price) {
        this.price = price;
        notifyObservers();
    }

    @Override
    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    @Override
    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    @Override
    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(price);
        }
    }
}

// Client code
public class StockMarketApp {
    public static void main(String[] args) {
        GoogleStock googleStock = new GoogleStock();
        
        Investor investor1 = new Investor("Alice");
        Investor investor2 = new Investor("Bob");

        googleStock.addObserver(investor1);
        googleStock.addObserver(investor2);

        // Google stock price updates
        googleStock.setPrice(1500.75f);
        googleStock.setPrice(1512.30f);
    }
}
```

#### Explanation:
- **Stock (`GoogleStock`)**: The subject that notifies its observers (investors) about price updates.
- **Investor (`Observer`)**: Observers that receive notifications whenever the stock price changes.
- **Real-time updates**: When the stock price changes, all registered observers (investors) are notified with the new price.

---

### Summary of Behavioral Patterns:
| Pattern                     | Purpose                                                          |
|-----------------------------|------------------------------------------------------------------|
| **Chain of Responsibility**  | Passes a request along a chain of handlers.                      |
| **Command**                  | Encapsulates requests as objects to enable undoable actions.     |
| **Interpreter**              | Defines a grammar and an interpreter for interpreting sentences. |
| **Iterator**                 | Sequentially accesses elements of a collection.                  |
| **Mediator**                 | Simplifies communication between classes through a mediator.     |
| **Memento**                  | Captures and restores an object’s state.                        |
| **Observer**                 | Notifies multiple objects of state changes in another object.    |
| **State**                    | Alters behavior when an object's internal state changes.         |
| **Strategy**                 | Defines interchangeable algorithms for a task.                  |
| **Template Method**          | Defines a skeleton for an algorithm and allows customization.    |
| **Visitor**                  | Adds new functionality to classes without modifying them.        |

Each pattern solves specific challenges related to communication, state management, and interaction between objects, making systems more modular and flexible.
------
