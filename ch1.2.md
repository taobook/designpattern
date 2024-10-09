# Factory

The Factory Method pattern is a creational design pattern that defines an interface for creating objects but allows subclasses to alter the type of objects that will be created. This pattern is particularly useful when a class cannot predict the class of objects it needs to create or when you want to localize the knowledge of which class to instantiate.

### Key Components

1. **Product**: This is the interface or abstract class that defines the type of object the factory method will create.
2. **Concrete Product**: These are the specific implementations of the product interface.
3. **Creator**: This is the abstract class or interface that declares the factory method, which returns a product.
4. **Concrete Creator**: These are the subclasses that implement the factory method to create specific products.

### Example Scenario

Let’s consider a simple example of a document management system where different types of documents can be created, such as `WordDocument` and `PDFDocument`.


### Step 1: Define the Product Interface

```java
// Product interface
public interface Document {
    void open();
}
```

### Step 2: Create Concrete Products

```java
// Concrete Product: WordDocument
public class WordDocument implements Document {
    @Override
    public void open() {
        System.out.println("Opening Word Document");
    }
}

// Concrete Product: PDFDocument
public class PDFDocument implements Document {
    @Override
    public void open() {
        System.out.println("Opening PDF Document");
    }
}
```

### Step 3: Define the Creator

```java
// Creator abstract class
public abstract class DocumentCreator {
    public abstract Document createDocument();
}
```

### Step 4: Create Concrete Creators

```java
// Concrete Creator: WordDocumentCreator
public class WordDocumentCreator extends DocumentCreator {
    @Override
    public Document createDocument() {
        return new WordDocument();
    }
}

// Concrete Creator: PDFDocumentCreator
public class PDFDocumentCreator extends DocumentCreator {
    @Override
    public Document createDocument() {
        return new PDFDocument();
    }
}
```

### Step 5: Client Code

```java
public class Client {
    public static void openDocument(DocumentCreator creator) {
        Document document = creator.createDocument();
        document.open();
    }

    public static void main(String[] args) {
        DocumentCreator wordCreator = new WordDocumentCreator();
        openDocument(wordCreator);  // Output: Opening Word Document

        DocumentCreator pdfCreator = new PDFDocumentCreator();
        openDocument(pdfCreator);  // Output: Opening PDF Document
    }
}
```

### Explanation

1. **Product Interface (`Document`)**: This defines the common interface for all document types.
2. **Concrete Products**: `WordDocument` and `PDFDocument` implement the `Document` interface and provide their own `open` methods.
3. **Creator Abstract Class**: `DocumentCreator` declares the factory method `createDocument`, which subclasses must implement.
4. **Concrete Creators**: `WordDocumentCreator` and `PDFDocumentCreator` implement the factory method to return instances of their respective document types.
5. **Client Code**: The `Client` class demonstrates how to use the creators to open different types of documents without knowing the specifics of the document classes.

### Advantages
- The client code is decoupled from the specific implementations of the documents, making it easy to add new document types by simply creating new concrete products and creators.
- It adheres to the Open/Closed Principle, allowing for extensions without modifying existing code.

This Java implementation effectively demonstrates the Factory Method pattern and its benefits!

### Advantages
- **Decoupling**: The client code does not need to know the details of the product classes; it only relies on the creator.
- **Flexibility**: New product types can be added easily by implementing new concrete creators without changing existing code.
- **Single Responsibility**: The creation logic is separated from the business logic.

### When to Use
- When a class cannot anticipate the class of objects it needs to create.
- When you want to localize the knowledge of which class to instantiate.
- When you have multiple classes with similar behavior but different implementations.

The Factory Method pattern promotes a clean and maintainable code structure, making it easier to manage object creation and adhere to the Open/Closed Principle.



传统方法，是将对象的创建由各自的调用者负责。工厂模式的主要思想是，将创建的功能封装在一个地方集中处理。


将对象的创建集中到一个地方， 这样，如果需要修改，只需要修改一个地方。
···java
class PizzaFactory {
	public static Pizza createPizza(){
		return null;
	}
}
···

没有工厂类，User只是先在自己的类中创建一个抽象的“方法”，再将对象的实例化推迟到子类的“方法”中实现


 

124）什么时候使用享元模式？(答案)
享元模式通过共享对象来避免创建太多的对象。为了使用享元模式，你需要确保你的对象是不可变的，这样你才能安全的共享。JDK 中 String 池、Integer 池以及 Long 池都是很好的使用了享元模式的例子。
