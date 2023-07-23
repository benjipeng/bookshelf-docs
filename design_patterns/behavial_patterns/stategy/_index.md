---
bookCollapseSection: false
weight: 20
---

# Strategy

The Strategy pattern is a ***behavioral design pattern*** that *enables* selecting an algorithm at runtime. Instead of implementing a single algorithm directly, code receives run-time instructions as to which in a family of algorithms to use. Here are the components of the Strategy pattern:

## Component

- **Strategy**: This is an interface common to all supported algorithms. Context uses this interface to call the algorithm defined by a ConcreteStrategy.

- **ConcreteStrategy**: This is a class that implements the Strategy interface.

- **Context**: This is a class that maintains a reference to a Strategy object, and uses that reference to call the algorithm defined by a ConcreteStrategy.
  
### Relationship

> The relationships between these components are as follows:

- The Context object is configured with a ConcreteStrategy object.
- The Context object maintains a reference to a Strategy object.
- The Context object delegates it to the Strategy object instead of implementing multiple versions of the algorithm on its own.

### Diagram

#### Mermaid Code

```c
classDiagram
    class Context{
        -strategy: Strategy
        +setStrategy(strategy: Strategy)
        +executeStrategy()
    }
    Context <|.. Strategy
    class Strategy{
        +execute()
    }
    Strategy <|.. ConcreteStrategyA
    Strategy <|.. ConcreteStrategyB
    class ConcreteStrategyA{
        +execute()
    }
    class ConcreteStrategyB{
        +execute()
    }
```

![stategy-pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/strategy-pattern.svg)

## Java Implementation

```java
// Strategy interface
interface Strategy {
    void execute();
}

// ConcreteStrategy classes
class ConcreteStrategyA implements Strategy {
    public void execute() {
        System.out.println("Executing strategy A");
    }
}

class ConcreteStrategyB implements Strategy {
    public void execute() {
        System.out.println("Executing strategy B");
    }
}

// Context class
class Context {
    private Strategy strategy;

    public Context(Strategy strategy) {
        this.strategy = strategy;
    }

    public void setStrategy(Strategy strategy) {
        this.strategy = strategy;
    }

    public void executeStrategy() {
        strategy.execute();
    }
}

// Main class
public class StrategyPatternDemo {
    public static void main(String[] args) {
        Strategy strategyA = new ConcreteStrategyA();
        Strategy strategyB = new ConcreteStrategyB();

        Context context = new Context(strategyA);
        context.executeStrategy();

        context.setStrategy(strategyB);
        context.executeStrategy();
    }
}
```

> In this example:

1. The Strategy interface defines a method execute() that encapsulates an algorithm.
2. The ConcreteStrategyA and ConcreteStrategyB classes implement the Strategy interface. Each class represents a different algorithm and provides its own implementation for the execute() method.
3. The Context class maintains a reference to a Strategy object, and uses that reference to call the algorithm defined by a ConcreteStrategy.

When you run the `StrategyPatternDemo`, it will *create* a **Context** object with an initial strategy of `ConcreteStrategyA`. It then executes this strategy, changes the strategy to `ConcreteStrategyB`, and executes the new strategy.

## Learn More

> Design patterns similar to the Strategy pattern include:

- **State Pattern**: Like the Strategy pattern, the State pattern can also be used to change the behavior of an object at runtime. However, the State pattern does this by changing the state of the object, while the Strategy pattern does it by changing the algorithm used.
- **Template Method Pattern**: The Template Method pattern defines the skeleton of an algorithm in a method, deferring some steps to subclasses. It lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure. While it's similar to the Strategy pattern in that it promotes flexibility, the Template Method pattern does this by allowing subclasses to redefine certain steps of an algorithm, while the Strategy pattern does it by encapsulating each algorithm inside a separate class.
- **Command Pattern**: The Command pattern turns a request into a stand-alone object that contains all information about the request. This transformation lets you pass requests as a method arguments, delay or queue a request's execution, and support undoable operations. The Command and Strategy patterns represent different ways of using polymorphism to achieve flexibility in designs.
