---
bookCollapseSection: false
weight: 20
---

# Template Method

The Template Method pattern is a behavioral design pattern that defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure. Here are the components of the Template Method pattern:

## Component

- **AbstractClass**: This is an abstract class that contains a template method and the definition of algorithm steps.
- **ConcreteClass**: This is a class that implements the abstract methods defined in the AbstractClass.

### Relationship

> The relationships between these components are as follows:

- The `AbstractClass` contains a method that defines the skeleton of an algorithm. This method is called the template method.
- The `template` method consists of calls to abstract methods, which are then implemented by the ConcreteClass.

### Diagram

#### Mermaid Code

```c
classDiagram
    AbstractClass <|.. ConcreteClass
    class AbstractClass{
        +templateMethod()
        +primitiveOperation1()
        +primitiveOperation2()
    }
    class ConcreteClass{
        +primitiveOperation1()
        +primitiveOperation2()
    }
```

![Template-Method-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/template-method-pattern.svg)

## Java Implementation

```java
// AbstractClass
abstract class AbstractClass {
    // Template method
    public void templateMethod() {
        primitiveOperation1();
        primitiveOperation2();
    }

    // Primitive operations
    public abstract void primitiveOperation1();
    public abstract void primitiveOperation2();
}

// ConcreteClass
class ConcreteClass extends AbstractClass {
    public void primitiveOperation1() {
        System.out.println("Primitive operation 1");
    }

    public void primitiveOperation2() {
        System.out.println("Primitive operation 2");
    }
}

// Main class
public class TemplateMethodPatternDemo {
    public static void main(String[] args) {
        AbstractClass abstractClass = new ConcreteClass();
        abstractClass.templateMethod();
    }
}
```

> In this example:

1. The AbstractClass defines a method templateMethod() that contains the skeleton of an algorithm. It also declares two abstract methods primitiveOperation1() and primitiveOperation2() that represent the steps of the algorithm.
2. The ConcreteClass extends AbstractClass and provides its own implementations for the primitiveOperation1() and primitiveOperation2() methods.

When you run the TemplateMethodPatternDemo, it will create an AbstractClass object (which is actually a ConcreteClass object) and call its templateMethod(). This will execute the algorithm defined in the templateMethod(), which in turn calls the primitiveOperation1() and primitiveOperation2() methods.

## Learn More

Strategy Pattern: Like the Template Method pattern, the Strategy pattern can also be used to change the behavior of an object at runtime. However, the Strategy pattern does this by encapsulating each algorithm inside a separate class, while the Template Method pattern does it by allowing subclasses to redefine certain steps of an algorithm.

Factory Method Pattern: The Factory Method pattern provides an interface for creating objects, but allows subclasses to alter the type of objects that will be created. The Factory Method pattern is similar to the Template Method pattern in that they both rely on a structure that delegates responsibility to subclasses.

Observer Pattern: The Observer pattern defines a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically. The Observer pattern is similar to the Template Method pattern in that it also defines a kind of algorithm (for notifying observers), but the details of that algorithm are defined in the individual observers.
