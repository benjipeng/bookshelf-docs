---
bookCollapseSection: false
weight: 20
---

# Abstract Factory

The Abstract Factory pattern is a ***creational design pattern*** that provides an interface for creating families of related or dependent objects without specifying their concrete classes. Here are the components of the Abstract Factory pattern:

## Component

- **AbstractFactory**: This is an `interface` that declares a set of methods that return different abstract products.
- **ConcreteFactory**: These are classes that implement the operations to create concrete products.
- **AbstractProduct**: These are `interfaces` for a family of product objects.
- **ConcreteProduct**: These are classes to define a product to be created.

### Relationship

> The relationships between these components are as follows:

- The AbstractFactory defines methods to create abstract products. Concrete factories implement these methods to create concrete products.
- Each ConcreteFactory corresponds to a specific variant of products and creates a set of products belonging to the same variant.
- AbstractProduct represents the abstract interfaces for products that make up a family of products. ConcreteProduct implements these interfaces.

### Diagram

![Abstract-Factory-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/abstract-factory-pattern.svg)

## Java Implementation

```java
// AbstractProductA
interface AbstractProductA {
}

// ProductA1
class ProductA1 implements AbstractProductA {
}

// ProductA2
class ProductA2 implements AbstractProductA {
}

// AbstractProductB
interface AbstractProductB {
}

// ProductB1
class ProductB1 implements AbstractProductB {
}

// ProductB2
class ProductB2 implements AbstractProductB {
}

// AbstractFactory
interface AbstractFactory {
    AbstractProductA createProductA();
    AbstractProductB createProductB();
}

// ConcreteFactory1
class ConcreteFactory1 implements AbstractFactory {
    public AbstractProductA createProductA() {
        return new ProductA1();
    }

    public AbstractProductB createProductB() {
        return new ProductB1();
    }
}

// ConcreteFactory2
class ConcreteFactory2 implements AbstractFactory {
    public AbstractProductA createProductA() {
        return new ProductA2();
    }

    public AbstractProductB createProductB() {
        return new ProductB2();
    }
}

// Main class
public class AbstractFactoryPatternDemo {
    public static void main(String[] args) {
        AbstractFactory factory1 = new ConcreteFactory1();
        AbstractProductA productA1 = factory1.createProductA();
        AbstractProductB productB1 = factory1.createProductB();

        AbstractFactory factory2 = new ConcreteFactory2();
        AbstractProductA productA2 = factory2.createProductA();
        AbstractProductB productB2 = factory2.createProductB();
    }
}
```

> In this example:

- The AbstractFactory interface declares methods for creating AbstractProductA and AbstractProductB.
ConcreteFactory1 and ConcreteFactory2 are concrete factories that implement the AbstractFactory interface and provide their own implementations for creating products.
- ProductA1, ProductA2, ProductB1, and ProductB2 are concrete products that implement the AbstractProductA and AbstractProductB interfaces respectively.
When you run the AbstractFactoryPatternDemo, it will create two AbstractFactory objects (which are actually ConcreteFactory1 and ConcreteFactory2 objects) and use them to create products.

## Learn More

1. Factory Method Pattern: Like the Abstract Factory pattern, the Factory Method pattern also provides an interface for creating objects. However, the Factory Method pattern does this by defining a method, and thus allows subclasses to change the class of the created object, while the Abstract Factory pattern does it by defining an interface for creating families of related objects.

2. Builder Pattern: The Builder pattern constructs complex objects step by step. It's similar to the Abstract Factory pattern in that it also abstracts the process of object creation, but it does so in a way that allows for more control over the construction process.

3. Prototype Pattern: The Prototype pattern creates objects by cloning an existing object. This pattern is similar to the Abstract Factory pattern in that it also abstracts the process of object creation, but it does so in a way that allows for more flexibility in the types of objects that can be created.

### Mermaid Code

> too long, therefore put in the end

```c
classDiagram
    AbstractFactory <|.. ConcreteFactory1
    AbstractFactory <|.. ConcreteFactory2
    AbstractProductA <|.. ProductA1
    AbstractProductA <|.. ProductA2
    AbstractProductB <|.. ProductB1
    AbstractProductB <|.. ProductB2
    class AbstractFactory{
        +createProductA()
        +createProductB()
    }
    class ConcreteFactory1{
        +createProductA()
        +createProductB()
    }
    class ConcreteFactory2{
        +createProductA()
        +createProductB()
    }
    class AbstractProductA{
    }
    class ProductA1{
    }
    class ProductA2{
    }
    class AbstractProductB{
    }
    class ProductB1{
    }
    class ProductB2{
    }
```
