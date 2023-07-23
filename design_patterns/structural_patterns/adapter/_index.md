---
bookCollapseSection: false
weight: 20
---

# Adapter

The Adapter pattern is a structural design pattern that allows objects with *incompatible* interfaces to collaborate. It's often used when you want to make your existing classes work with others without modifying their source code. Here are the components of the Adapter pattern:

## Component

- **Target**: This is the interface that clients use.
- **Adapter**: This is a class that can translate the interface of one class into an interface expected by the clients.
- **Adaptee**: This is the class that needs adapting. It contains some useful behavior, but its interface isn't compatible with the existing client code.
- **Client**: This is a class that contains the existing application code that needs to interact with the Adaptee.

### Relationship

> The relationships between these components are as follows:

1. The Client interacts with a Target object. The Target interface is compatible with the Client code.
2. The Adapter class implements the Target interface and contains a reference to an Adaptee object.
3. The Client invokes methods on the Adapter object. The Adapter calls Adaptee's methods to perform the operations.

### Diagram

#### Mermaid Code

![Adapter-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/adapter-pattern.svg)

## Java Implementation

```java
// Target interface
interface Target {
    void request();
}

// Adaptee class
class Adaptee {
    void specificRequest() {
        System.out.println("Executing specific request");
    }
}

// Adapter class
class Adapter implements Target {
    private Adaptee adaptee;

    public Adapter(Adaptee adaptee) {
        this.adaptee = adaptee;
    }

    public void request() {
        adaptee.specificRequest();
    }
}

// Client class
public class AdapterPatternDemo {
    public static void main(String[] args) {
        Adaptee adaptee = new Adaptee();
        Target target = new Adapter(adaptee);
        target.request();
    }
}
```

The Target interface defines a method request() that the client code expects to use.
The Adaptee class has a method specificRequest() that needs adapting to be used by the client code.
The Adapter class implements the Target interface and contains a reference to an Adaptee object. It adapts the interface of Adaptee to the Target interface.

When you run the AdapterPatternDemo, it will create an Adaptee object, an Adapter object that wraps the Adaptee, and then calls the request() method on the Adapter, which in turn calls the specificRequest() method on the Adaptee.

## Learn More

> Design patterns similar to the Adapter pattern include:

1. Bridge Pattern: Like the Adapter pattern, the Bridge pattern also allows two components to work together even if their interfaces are not compatible. However, the Bridge pattern is used up-front in a design to let abstractions and implementations vary independently, while the Adapter pattern is used to make existing classes work together after they were designed without such consideration.

2. Decorator Pattern: The Decorator pattern also involves a set of decorator classes that are used to wrap concrete components. Decorator classes mirror the type of the components they decorate but add or override behavior. The key difference is that the Decorator pattern extends the behavior of an object, while the Adapter pattern allows its interface to be used by other code.

3. Facade Pattern: The Facade pattern provides a simplified interface to a complex subsystem. While it may wrap multiple classes, its purpose is to simplify the interface, not to adapt different interfaces.

```c
classDiagram
    direction LR
    Client --|> Target 
    Target <|.. Adapter
    Adapter --|> Adaptee
    class Client{
        +request()
    }
    class Target{
        +request()
    }
    class Adapter{
        -adaptee: Adaptee
        +request()
    }
    class Adaptee{
        +specificRequest()
    }
```
