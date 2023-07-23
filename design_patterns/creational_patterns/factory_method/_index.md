---
bookCollapseSection: false
weight: 20
---

# Factory Method

The Factory Method pattern is a ***creational design pattern*** that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created. Here are the components of the Factory Method pattern:

## Component

1. **Creator**: This is an abstract class that declares the factory method, which returns an object of the Product class. The Creator class also often contains some core business logic that relies on Product objects returned by the factory method.
2. **ConcreteCreator**: These are classes that implement the factory method to produce products. The factory method returns a Product object, but the exact type of the product is determined by the ConcreteCreator.
3. **Product**: This is an abstract interface for the products that are being created.
4. **ConcreteProduct**: These are the specific products that the factory method creates.

### Relationship

> The relationships between these components are as follows:

- The Creator class declares the factory method that returns new product objects. The return type of this method is Product, which is a common interface for all products.
- The ConcreteCreator classes override the factory method to change the resulting product's type.

Product is the common product interface, and ConcreteProduct is a concrete product that implements the Product interface.

### Diagram

![Factory-Method-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/factory-method-pattern.svg)

## Java Implementation

```java
// Product
interface Product {
}

// ConcreteProduct
class ConcreteProduct implements Product {
}

// Creator
abstract class Creator {
    public abstract Product factoryMethod();
}

// ConcreteCreator
class ConcreteCreator extends Creator {
    public Product factoryMethod() {
        return new ConcreteProduct();
    }
}

// Main class
public class FactoryMethodPatternDemo {
    public static void main(String[] args) {
        Creator creator = new ConcreteCreator();
        Product product = creator.factoryMethod();
    }
}
```

*In this example:*

- The `Product` `interface` represents the product that the factory method will create.
- `ConcreteProduct` is a concrete product that *implements* the Product interface.
- The `Creator` `abstract class` declares the factory method, which returns a Product object.
- `ConcreteCreator` is a concrete creator that extends the Creator abstract class and overrides the factory method to return a `ConcreteProduct`.

When you run the FactoryMethodPatternDemo, it will create a ConcreteCreator object and use it to create a Product object.

## Learn More

> Design patterns similar to the Factory Method pattern include:

- **Abstract Factory** Pattern: Like the Factory Method pattern, the Abstract Factory pattern also provides an interface for creating objects. However, the Abstract Factory pattern does this by defining an interface for creating families of related objects, while the Factory Method pattern does it by defining a method, and thus allows subclasses to change the class of the created object.

- **Builder** Pattern: The Builder pattern constructs complex objects step by step. It's similar to the Factory Method pattern in that it also abstracts the process of object creation, but it does so in a way that allows for more control over the construction process.

- **Prototype** Pattern: The Prototype pattern creates objects by cloning an existing object. This pattern is similar to the Factory Method pattern in that it also abstracts the process of object creation, but it does so in a way that allows for more flexibility in the types of objects that can be created.

### Mermaid Code

```c
classDiagram
    Creator <|.. ConcreteCreator
    Product <|.. ConcreteProduct
    class Creator{
        +factoryMethod(): Product
    }
    class ConcreteCreator{
        +factoryMethod(): Product
    }
    class Product{
    }
    class ConcreteProduct{
    }
```
