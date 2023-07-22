---
bookCollapseSection: false
weight: 20
---

# Strategy

## Component

### Originator / Memento / Caretaker

### Relationship

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

![Factory-Method-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/strategy-pattern.svg)

## Java Implementation

## Learn More
