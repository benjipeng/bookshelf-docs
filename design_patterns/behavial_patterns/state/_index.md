---
bookCollapseSection: false
weight: 20
---

# State

The State pattern is a **behavioral design pattern** that allows an object to *change* its behavior when its internal state changes. The object will appear to change its class.

## Components of the State pattern

1. ***State***: This is an interface that defines a method to handle the requests, which should be implemented by all the concrete states.

2. ***ConcreteState***: These are classes that implement the State interface. Each class represents a different state and provides its own implementation for the request.

3. ***Context***: This is a class that maintains an instance of a ConcreteState subclass that defines the current state of the object.

### Relationship

> The relationships between these components are as follows:

- The **Context** delegates the request to the state object to handle it.
- The **State** provides an interface for encapsulating the behavior associated with a particular state of the Context.
- **ConcreteState** each subclass *implements* a behavior *associated* with a state of Context.

### Diagram

#### Mermaid Code

```c
classDiagram
    direction LR
    Context o-- State
    State <|.. ConcreteState
    class Context{
        +request()
        +setState(state: State)
    }
    class State{
        +handle(context: Context)
    }
    class ConcreteState{
        +handle(context: Context)
    }
```

![State-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/state-pattern.svg)

## Java Implementation

```java
// State interface
interface State {
    void handle(Context context);
}

// ConcreteState classes
class ConcreteStateA implements State {
    public void handle(Context context) {
        System.out.println("Handling in ConcreteStateA");
        context.setState(new ConcreteStateB());
    }
}

class ConcreteStateB implements State {
    public void handle(Context context) {
        System.out.println("Handling in ConcreteStateB");
        context.setState(new ConcreteStateA());
    }
}

// Context class
class Context {
    private State state;

    public Context(State state) {
        this.state = state;
    }

    public void setState(State state) {
        this.state = state;
    }

    public void request() {
        state.handle(this);
    }
}

// Main class
public class StatePatternDemo {
    public static void main(String[] args) {
        Context context = new Context(new ConcreteStateA());

        context.request();
        context.request();
    }
}
```

### Details

> In this example:

- The State interface defines a method handle() that each state uses to handle the request from the Context.
- ConcreteStateA and ConcreteStateB are concrete states that implement the State interface. Each provides its own implementation of the handle() method and changes the current state of the Context.
- The Context class maintains a reference to the current state and delegates the request to the current state's handle() method.
  
When you run the StatePatternDemo, it will create a Context with an initial state of ConcreteStateA. It then makes two requests to the Context, and you will see the state change between ConcreteStateA and ConcreteStateB.

## Learn More

> Design patterns similar to the State pattern include:

1. **Strategy Pattern**: Like the State pattern, the Strategy pattern can also be used to change the behavior of an object at runtime. However, the Strategy pattern does this by changing the algorithm used, while the State pattern changes the state of the object.

2. **Bridge Pattern**: The Bridge pattern is a structural pattern, unlike the State pattern which is a behavioral pattern. The Bridge pattern is used to separate an abstraction from its implementation so that the two can vary independently. The State pattern, on the other hand, allows an object to alter its behavior when its internal state changes.

3. **Command Pattern**: The Command pattern encapsulates a request as an object, thereby letting you parameterize other objects with different requests, queue or log requests, and support undoable operations. It's different from the State pattern which is about changing behavior when an object's state changes.
