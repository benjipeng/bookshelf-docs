---
bookCollapseSection: false
weight: 20
---

# Command

The Command pattern is a **behavioral design pattern** that turns a *request* into a *stand-alone* object that contains all information about the request. This transformation lets you pass requests as a method arguments, delay or queue a request's execution, and support undoable operations. Here are the components of the Command pattern:

## Component

- **Command**: This is an interface that declares a method for a particular action.

- **ConcreteCommand**: This is a class that defines a binding between a Receiver object and an action. It implements the Command interface and overrides the execute method.

- **Invoker**: This is a class that asks the command to carry out the request.

- **Receiver**: This is a class that performs the action associated with the request.

### Relationship

> The relationships between these components are as follows:

- The `Invoker` object is associated with one or several commands. It sends a request to the command to execute the necessary operations.
- The `ConcreteCommand` object is linked to a Receiver object and invokes methods on the receiver in response to execute() calls.

### Diagram

#### Mermaid Code

```c
classDiagram
    Invoker <|.. Command
    Command <|.. ConcreteCommand
    Receiver -- ConcreteCommand
    class Invoker{
        +setCommand(command: Command)
        +executeCommand()
    }
    class Command{
        +execute()
    }
    class ConcreteCommand{
        -receiver: Receiver
        +execute()
    }
    class Receiver{
        +action()
    }
```

![Factory-Method-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/memento-pattern.svg)

## Java Implementation

```java
// Command interface
interface Command {
    void execute();
}

// ConcreteCommand classes
class ConcreteCommand1 implements Command {
    private Receiver receiver;

    public ConcreteCommand1(Receiver receiver) {
        this.receiver = receiver;
    }

    public void execute() {
        receiver.action1();
    }
}

class ConcreteCommand2 implements Command {
    private Receiver receiver;

    public ConcreteCommand2(Receiver receiver) {
        this.receiver = receiver;
    }

    public void execute() {
        receiver.action2();
    }
}

// Receiver class
class Receiver {
    public void action1() {
        System.out.println("Performing action 1");
    }

    public void action2() {
        System.out.println("Performing action 2");
    }
}

// Invoker class
class Invoker {
    private Command command;

    public void setCommand(Command command) {
        this.command = command;
    }

    public void executeCommand() {
        command.execute();
    }
}

// Main class
public class CommandPatternDemo {
    public static void main(String[] args) {
        Receiver receiver = new Receiver();
        Command command1 = new ConcreteCommand1(receiver);
        Command command2 = new ConcreteCommand2(receiver);

        Invoker invoker = new Invoker();
        invoker.setCommand(command1);
        invoker.executeCommand();

        invoker.setCommand(command2);
        invoker.executeCommand();
    }
}
```

> Herein,

- The `Command` *interface* defines a method `execute()` that *encapsulates* an action and its parameters.
- The `ConcreteCommand1` and `ConcreteCommand2` classes implement the Command interface. Each class represents a *different* operation and provides its own implementation for the execute() method.
- The `Receiver` class performs the ***actual*** actions.
- The `Invoker` class asks the command to execute the request.
  
When you run the `CommandPatternDemo`, it will create a Receiver object and two Command objects. The Invoker then executes these commands in order.

## Learn More

> Design patterns similar to the Command pattern include:

- **Strategy Pattern**: Like the Command pattern, the Strategy pattern can also be used to change the behavior of an object at runtime. However, the Strategy pattern does this by changing the algorithm used, while the Command pattern does it by encapsulating a request as an object.

- **Chain of Responsibility Pattern**: The Chain of Responsibility pattern is similar to the Command pattern in that they both build a chain of objects that can handle a request. However, in the Chain of Responsibility pattern, the request is passed along the chain until an object handles it, while in the Command pattern, the request is encapsulated as an object and given to a specific handler.

- **Observer Pattern**: The Observer pattern defines a ***one-to-many*** dependency between objects so that when one object changes state, all its dependents are notified and updated automatically. The Command pattern is similar in that it also encapsulates a change in state (as a request) and passes it to another object. However, the Command pattern is more about action and control, while the Observer pattern is about state and data.
