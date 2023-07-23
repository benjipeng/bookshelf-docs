---
bookCollapseSection: false
weight: 20
---

# Decorator

The `Decorator` pattern is a ***structural*** design pattern that allows adding *new* behaviors to objects dynamically by placing these objects inside special ***wrapper*** objects. Using decorators, you can *stack* behaviors *dynamically*, as they can *wrap* not only simple components but also other decorators. Here are the components of the Decorator pattern:

## Component

1. **Component**: This is an ***interface*** for objects that can have responsibilities added to them *dynamically*.

2. **ConcreteComponent**: This is a ***class*** that *implements* the `Component` interface.

3. **Decorator**: This is an ***abstract class*** that *implements* the `Component` interface and maintains a reference to a `Component` object. It forwards requests to the `Component` object and can optionally perform additional operations before or after forwarding.

4. **ConcreteDecorator**: This is a class that extends the Decorator class and adds responsibilities to the `Component`.

### Relationship

- The `Decorator` class maintains a *reference* to a Component object and defines an interface that *conforms* to the Component's interface.
- The `ConcreteDecorator` class *extends* the Decorator class and adds responsibilities to the Component.

### Diagram

![Decorator-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/decorator-pattern.svg)

## Java Implementation

```java
// Component interface
interface Component {
    void operation();
}

// ConcreteComponent class
class ConcreteComponent implements Component {
    public void operation() {
        System.out.println("Executing operation in ConcreteComponent");
    }
}

// Decorator abstract class
abstract class Decorator implements Component {
    protected Component component;

    public Decorator(Component component) {
        this.component = component;
    }

    public void operation() {
        component.operation();
    }
}

// ConcreteDecorator classes
class ConcreteDecoratorA extends Decorator {
    public ConcreteDecoratorA(Component component) {
        super(component);
    }

    public void operation() {
        System.out.println("Executing operation in ConcreteDecoratorA");
        super.operation();
    }
}

class ConcreteDecoratorB extends Decorator {
    public ConcreteDecoratorB(Component component) {
        super(component);
    }

    public void operation() {
        System.out.println("Executing operation in ConcreteDecoratorB");
        super.operation();
    }
}

// Main class
public class DecoratorPatternDemo {
    public static void main(String[] args) {
        Component component = new ConcreteComponent();
        Component decoratorA = new ConcreteDecoratorA(component);
        Component decoratorB = new ConcreteDecoratorB(decoratorA);

        decoratorB.operation();
    }
}
```

> In this example:

- The `Component` interface defines a method `operation()` that encapsulates an operation.
- The `ConcreteComponent` class *implements* the `Component` interface and provides its own implementation for the operation() method.
- The `Decorator` abstract class *implements* the `Component` interface and maintains a reference to a `Component` object. It uses that reference to call the operation defined by a `Component`.
- The `ConcreteDecoratorA` and `ConcreteDecoratorB` classes *extend* the `Decorator` *abstract* class. Each class represents a different decorator and provides its own implementation for the operation() method.

When you run the DecoratorPatternDemo, it will create a `ConcreteComponent` object, wrap it with a `ConcreteDecoratorA`, then wrap the result with a `ConcreteDecoratorB`, and finally call the operation() method on the resulting object.

## Learn More

1. **Composite Pattern**: Like the Decorator pattern, the Composite pattern is also a structural design pattern that allows treating individual objects and compositions of objects uniformly. However, the Composite pattern does this by allowing an object to be treated as a single instance of an object or as a group of objects.

2. **Chain of Responsibility Pattern**: The Chain of Responsibility pattern is a behavioral design pattern that allows passing request along the chain of potential handlers until one of them handles the request. It's similar to the Decorator pattern in that it promotes flexibility and loose coupling, but it does this by decoupling sender and receiver of a request.

3. **Adapter Pattern**: The Adapter pattern is a structural design pattern that allows objects with incompatible interfaces to collaborate. It's similar to the Decorator pattern in that it wraps an object, but the Adapter pattern does this to change the object's interface, while the Decorator pattern does it to add new behaviors.

### Mermaid Code

```c
classDiagram
    Component <|.. ConcreteComponent
    Component <|.. Decorator
    Decorator <|.. ConcreteDecoratorA
    Decorator <|.. ConcreteDecoratorB
    class Component{
        +operation(): void
    }
    class ConcreteComponent{
        +operation(): void
    }
    class Decorator{
        -component: Component
        +Decorator(component: Component)
        +operation(): void
    }
    class ConcreteDecoratorA{
        +operation(): void
    }
    class ConcreteDecoratorB{
        +operation(): void
    }
```
