---
bookCollapseSection: false
weight: 20
---

# Fly Weight

The `Flyweight` pattern is a *structural* design pattern that lets you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object. Here are the components of the Flyweight pattern:

## Component

1. **Flyweight**: This is an interface through which flyweights can receive and act on extrinsic states.

2. **ConcreteFlyweight**: This class implements the Flyweight interface and adds storage for intrinsic state, if any. ConcreteFlyweight objects must be sharable. Any state they store must be intrinsic; that is, it must be independent of the ConcreteFlyweight object's context.

3. **FlyweightFactory**: This class creates and manages flyweight objects. It ensures that flyweights are shared properly. When a client requests a flyweight, the FlyweightFactory supplies an existing instance or creates one, if none exists.

4. **Client**: This class maintains references to flyweights and computes or stores the extrinsic state of flyweights.

### Relationship

> The relationships between these components are as follows:

- The `Client` object interacts with the `FlyweightFactory` to request a `Flyweight` object.
- The `FlyweightFactory` object creates a new `ConcreteFlyweight` object or returns an existing one, depending on whether the requested `Flyweight` object exists.
- The `Client` object interacts with the `Flyweight` object through the `Flyweight` interface.

### Diagram

![Fly-Weight-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/flyweight-pattern.svg)

## Java Implementation

```java
import java.util.HashMap;
import java.util.Map;

// The Flyweight interface
interface Flyweight {
    void operation(String extrinsicState);
}

// A ConcreteFlyweight class
class ConcreteFlyweight implements Flyweight {
    private String intrinsicState;

    public ConcreteFlyweight(String intrinsicState) {
        this.intrinsicState = intrinsicState;
    }

    public void operation(String extrinsicState) {
        System.out.println("Intrinsic State = " + this.intrinsicState);
        System.out.println("Extrinsic State = " + extrinsicState);
    }
}

// The FlyweightFactory class
class FlyweightFactory {
    private Map<String, Flyweight> flyweights = new HashMap<>();

    public Flyweight getFlyweight(String key) {
        if (!flyweights.containsKey(key)) {
            flyweights.put(key, new ConcreteFlyweight(key));
        }
        return flyweights.get(key);
    }
}

// The Client class
public class FlyweightPatternDemo {
    public static void main(String[] args) {
        FlyweightFactory factory = new FlyweightFactory();

        Flyweight flyweight1 = factory.getFlyweight("A");
        flyweight1.operation("First Call");

        Flyweight flyweight2 = factory.getFlyweight("A");
        flyweight2.operation("Second Call");

        Flyweight flyweight3 = factory.getFlyweight("B");
        flyweight3.operation("Third Call");
    }
}
```

> In this example:

- The Flyweight interface defines a method operation() that encapsulates an operation that uses extrinsic state.
- The ConcreteFlyweight class implements the Flyweight interface. It represents a flyweight object that can be shared. It maintains intrinsic state that must be independent of the flyweight object's context.
- The FlyweightFactory class creates and manages flyweight objects. It ensures that flyweights are shared properly. When a client requests a flyweight, the FlyweightFactory supplies an existing instance or creates one if none exists.
- The FlyweightPatternDemo (Client) class maintains references to flyweights and computes or stores the extrinsic state of flyweights.

When you run the `FlyweightPatternDemo`, it will create a ***FlyweightFactory*** object, and then make three *requests* for *flyweights*. The first two requests ask for a flyweight with key "A", and the third request asks for a flyweight with key "B". The FlyweightFactory returns the same flyweight for the first two requests, and a different flyweight for the third request.

## Learn More

**Composite Pattern**: The Composite pattern composes objects into tree structures to represent part-whole hierarchies. It lets clients treat individual objects and compositions of objects uniformly. While the Composite pattern focuses on building complex structures, the Flyweight pattern focuses on efficient sharing of objects to reduce memory usage.

**Decorator Pattern**: The Decorator pattern attaches new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors. Like the Flyweight pattern, the Decorator pattern is a structural pattern that involves a set of decorator classes that are used to wrap concrete classes. However, the Decorator pattern focuses on adding behaviors to objects, while the Flyweight pattern focuses on sharing objects to save memory.

**Singleton Pattern**: The Singleton pattern ensures that a class has only one instance, and provides a global point of access to it. Like the Flyweight pattern, the Singleton pattern involves a single instance, but the purpose of the Singleton pattern is to ensure only one instance of a class exists, while the purpose of the Flyweight pattern is to share objects to save memory.

### Mermaid Code

```c
classDiagram
    direction LR
    FlyweightFactory <|.. Flyweight
    Flyweight <|.. ConcreteFlyweight
    Client -- FlyweightFactory
    class FlyweightFactory{
        -flyweights: Map
        +getFlyweight(key: String): Flyweight
    }
    class Flyweight{
        +operation(extrinsicState: String)
    }
    class ConcreteFlyweight{
        -intrinsicState: String
        +operation(extrinsicState: String)
    }
    class Client{
        -factory: FlyweightFactory
        +Client(factory: FlyweightFactory)
        +execute()
    }
```
