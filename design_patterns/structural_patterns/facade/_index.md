---
bookCollapseSection: false
weight: 20
---

# Facade

The Facade pattern is a ***structural*** design pattern that provides a simplified **interface** to a library, a framework, or any other complex set of classes. Here are the components of the Facade pattern:

## Component

1. **Facade**: This is a class that provides a simple interface to a complex subsystem. It contains references to the subsystem's objects and delegates client requests to these objects.

2. **Subsystem**: These are classes that implement subsystem functionality. They handle work assigned by the Facade object and have no knowledge of the facade.

3. **Client**: This is a class that uses the Facade instead of calling subsystem objects directly.

### Relationship

- The Client object uses the Facade to interact with the subsystems.
- The Facade delegates client requests to appropriate subsystem objects.
- The subsystem classes perform the actual work, unaware of the facade.

### Diagram

![Facade-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/facade-pattern.svg)

## Java Implementation

```java
// Subsystem classes
class Subsystem1 {
    public void operation1() {
        System.out.println("Subsystem1 operation");
    }
}

class Subsystem2 {
    public void operation2() {
        System.out.println("Subsystem2 operation");
    }
}

// Facade class
class Facade {
    private Subsystem1 subsystem1;
    private Subsystem2 subsystem2;

    public Facade() {
        this.subsystem1 = new Subsystem1();
        this.subsystem2 = new Subsystem2();
    }

    public void execute() {
        subsystem1.operation1();
        subsystem2.operation2();
    }
}

// Client class
public class FacadePatternDemo {
    public static void main(String[] args) {
        Facade facade = new Facade();
        facade.execute();
    }
}
```

> In this example:

- The Subsystem1 and Subsystem2 classes represent different subsystems. Each class has a method (operation1 and operation2) that performs an operation.

- The Facade class provides a simplified interface to the subsystems. It maintains references to the subsystem objects and delegates client requests to these objects.

- The FacadePatternDemo (client) uses the Facade to interact with the subsystems.

When you run the FacadePatternDemo, it will create a Facade object and call the execute method. This method in turn calls the operations of the subsystems.

## Learn More

> Design patterns similar to the Facade pattern include:

**Adapter Pattern**: Like the Facade pattern, the Adapter pattern is also used to simplify the interface of a class or a group of classes. However, while the Facade pattern is used to provide a simple interface to a complex subsystem, the Adapter pattern is used to convert the interface of a class into another interface that clients expect.

**Mediator Pattern**: The Mediator pattern is similar to the Facade pattern in that it abstracts functionality of existing classes. However, the Mediator pattern adds a level of indirection by having existing classes refer to the mediator, instead of referring to each other directly.

**Composite Pattern**: The Composite pattern is used to simplify the use of groups of objects. While it's similar to the Facade pattern in that it promotes simplicity, the Composite pattern does this by treating groups of objects and individual objects the same, while the Facade pattern does it by providing a simplified interface to a complex subsystem.

### Mermaid Code

```c
classDiagram
    direction LR
    Client --|> Facade
    Facade --|> Subsystem1
    Facade --|> Subsystem2
    class Client{
    }
    class Facade{
        -subsystem1: Subsystem1
        -subsystem2: Subsystem2
        +setSubsystem1(subsystem1: Subsystem1)
        +setSubsystem2(subsystem2: Subsystem2)
        +execute()
    }
    class Subsystem1{
        +operation1()
    }
    class Subsystem2{
        +operation2()
    }
```
