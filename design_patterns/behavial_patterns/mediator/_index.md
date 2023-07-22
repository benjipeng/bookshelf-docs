---
bookCollapseSection: false
weight: 20
---

# Mediator

The Mediator pattern is a behavioral design pattern that reduces coupling between components of a program by making them communicate indirectly, through a special mediator object. The Mediator makes it easy to modify, extend and reuse individual components because they’re no longer dependent on the dozens of other classes.

```c
classDiagram
    Mediator <|.. ConcreteMediator
    Mediator : +void send(String message, Colleague colleague)
    ConcreteMediator : +void send(String message, Colleague colleague)
    Colleague <|.. ConcreteColleague1
    Colleague <|.. ConcreteColleague2
    Colleague : +void send(String message)
    Colleague : +void receive(String message)
    ConcreteColleague1 : +void send(String message)
    ConcreteColleague1 : +void receive(String message)
    ConcreteColleague2 : +void send(String message)
    ConcreteColleague2 : +void receive(String message)
    ConcreteMediator o-- ConcreteColleague1
    ConcreteMediator o-- ConcreteColleague2
```

![mediator-pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/mediator-pattern.svg)

In this diagram, the Mediator `interface` is *implemented* by the ConcreteMediator class. The Colleague `abstract class` is *extended* by ConcreteColleague1 and ConcreteColleague2. The ConcreteMediator has *associations* with ConcreteColleague1 and ConcreteColleague2.

The Mediator pattern involves four types of classes:

- **Mediator**: This is an interface that defines a method for communicating with colleagues.
- **ConcreteMediator**: This is a class that implements the Mediator interface and coordinates communication between colleague objects. It's aware of all the colleagues and their purpose with regards to intercommunication.
- **Colleague**: This is an abstract class that maintains a reference to a Mediator object.
- **ConcreteColleague**: These are the classes that extend the Colleague class. Each colleague communicates with its mediator whenever it would have otherwise communicated with another colleague.

```java
// Mediator.java
public interface Mediator {
    void send(String message, Colleague colleague);
}

// ConcreteMediator.java
public class ConcreteMediator implements Mediator {
    private ConcreteColleague1 colleague1;
    private ConcreteColleague2 colleague2;

    public void setColleague1(ConcreteColleague1 colleague1) {
        this.colleague1 = colleague1;
    }

    public void setColleague2(ConcreteColleague2 colleague2) {
        this.colleague2 = colleague2;
    }

    public void send(String message, Colleague colleague) {
        if (colleague == colleague1) {
            colleague2.receive(message);
        } else {
            colleague1.receive(message);
        }
    }
}

// Colleague.java
public abstract class Colleague {
    protected Mediator mediator;

    public Colleague(Mediator mediator) {
        this.mediator = mediator;
    }

    public abstract void send(String message);
    public abstract void receive(String message);
}

// ConcreteColleague1.java
public class ConcreteColleague1 extends Colleague {
    public ConcreteColleague1(Mediator mediator) {
        super(mediator);
    }

    public void send(String message) {
        mediator.send(message, this);
    }

    public void receive(String message) {
        System.out.println("Colleague1 received: " + message);
    }
}

// ConcreteColleague2.java
public class ConcreteColleague2 extends Colleague {
    public ConcreteColleague2(Mediator mediator) {
        super(mediator);
    }

    public void send(String message) {
        mediator.send(message, this);
    }

    public void receive(String message) {
        System.out.println("Colleague2 received: " + message);
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        ConcreteMediator mediator = new ConcreteMediator();

        ConcreteColleague1 colleague1 = new ConcreteColleague1(mediator);
        ConcreteColleague2 colleague2 = new ConcreteColleague2(mediator);

        mediator.setColleague1(colleague1);
        mediator.setColleague2(colleague2);

        colleague1.send("Hello, Colleague2!");
        colleague2.send("Hello, Colleague1!");
    }
}
```

In this example, `ConcreteColleague1` and `ConcreteColleague2` are sending messages to each other via the `ConcreteMediator`. The `ConcreteMediator` knows how to route the messages so that they reach the correct recipient.

The **Mediator** pattern is similar to the **Observer** pattern in that both promote loose coupling and encapsulate complex interactions. The *key* difference is that the *Observer pattern allows objects to directly communicate with each other*, while the *Mediator pattern centralizes communication between objects* so they don't communicate with each other directly. The Mediator pattern is useful when there's complex communication between a set of objects that is difficult to understand or maintain.
