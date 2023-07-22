---
bookCollapseSection: false
weight: 20
---

# Visitor

The Visitor pattern is a way of ***separating an algorithm from an object structure on which it operates***. It allows you to add new operations to existing object structures *without* modifying those structures. It's useful when you have to perform several unrelated operations across the classes.

## Composition

The main components of the Visitor pattern are:

- **Element (Abstract Class)**: This is an interface which declares a accept method that takes the visitor object as an argument.

- **ConcreteElement (Class)**: These classes implement the Element interface and define the accept method. The visitor object is passed to this method.

- **Visitor (Interface)**: This is an interface that declares a visit operation for each class of ConcreteElement. The name and argument of the visit operations can differ.

- **ConcreteVisitor (Class)**: This class implements each operation declared by the Visitor. Each operation implements a fragment of the algorithm needed for the corresponding class of object.

### Diagram

#### Code

```c
classDiagram
    class Element {
        +accept(v: Visitor)
    }
    class ConcreteElementA {
        +accept(v: Visitor)
        +operationA()
    }
    class ConcreteElementB {
        +accept(v: Visitor)
        +operationB()
    }
    class Visitor {
        +visitConcreteElementA(e: ConcreteElementA)
        +visitConcreteElementB(e: ConcreteElementB)
    }
    class ConcreteVisitor {
        +visitConcreteElementA(e: ConcreteElementA)
        +visitConcreteElementB(e: ConcreteElementB)
    }
    Element <|-- ConcreteElementA
    Element <|-- ConcreteElementB
    Visitor <|-- ConcreteVisitor
    ConcreteElementA o-- ConcreteVisitor : accepts >
    ConcreteElementB o-- ConcreteVisitor : accepts >
```

#### Details

![visitor-pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/visitor-pattern.svg)

In the diagram:

- **Element** is the element interface.
- **ConcreteElementA** and ConcreteElementB are concrete elements.
- **Visitor** is the visitor interface.
- **ConcreteVisitor** is a concrete visitor.
  
The arrows show the relationships between these components. The "accepts" arrows from ConcreteElementA and ConcreteElementB to ConcreteVisitor represent the accept method in the concrete elements that takes a visitor as an argument.

## Java Example

### `Element` and `ConcreteElement`s

First, let's define the ComputerPart interface (our Element):

```java
public interface ComputerPart {
    public void accept(ComputerPartVisitor computerPartVisitor);
}
```

Next, we'll create concrete classes for different parts of the computer (our ConcreteElements):

```java
public class Keyboard implements ComputerPart {
    @Override
    public void accept(ComputerPartVisitor computerPartVisitor) {
        computerPartVisitor.visit(this);
    }
}

public class Monitor implements ComputerPart {
    @Override
    public void accept(ComputerPartVisitor computerPartVisitor) {
        computerPartVisitor.visit(this);
    }
}

public class Mouse implements ComputerPart {
    @Override
    public void accept(ComputerPartVisitor computerPartVisitor) {
        computerPartVisitor.visit(this);
    }
}

public class Computer implements ComputerPart {
    ComputerPart[] parts;

    public Computer() {
        parts = new ComputerPart[] {new Mouse(), new Keyboard(), new Monitor()};
    }

    @Override
    public void accept(ComputerPartVisitor computerPartVisitor) {
        for (int i = 0; i < parts.length; i++) {
            parts[i].accept(computerPartVisitor);
        }
        computerPartVisitor.visit(this);
    }
}
```

### `Visitor` and `ConcreteVisitor`

Now, let's define the ComputerPartVisitor interface (our Visitor):

```java
public interface ComputerPartVisitor {
    public void visit(Computer computer);
    public void visit(Mouse mouse);
    public void visit(Keyboard keyboard);
    public void visit(Monitor monitor);
}
```

And a concrete visitor class (our ConcreteVisitor):

```java
public class ComputerPartDisplayVisitor implements ComputerPartVisitor {
    @Override
    public void visit(Computer computer) {
        System.out.println("Displaying Computer.");
    }

    @Override
    public void visit(Mouse mouse) {
        System.out.println("Displaying Mouse.");
    }

    @Override
    public void visit(Keyboard keyboard) {
        System.out.println("Displaying Keyboard.");
    }

    @Override
    public void visit(Monitor monitor) {
        System.out.println("Displaying Monitor.");
    }
}
```

### Main

```java
public class VisitorPatternDemo {
    public static void main(String[] args) {
        ComputerPart computer = new Computer();
        computer.accept(new ComputerPartDisplayVisitor());
    }
}
```

## Learn More

As for other design patterns similar to the Visitor, they include the Strategy and State patterns. The Strategy pattern is similar in that it allows you to change the behavior of an object at runtime, but it doesn't require the object structure to be fixed. The State pattern is similar in that it allows an object to change its behavior when its internal state changes, but it doesn't involve separate visitor objects. The use case differences mainly lie in whether you need to perform operations across a fixed object structure (Visitor), need to change an object's behavior at runtime (Strategy), or need an object to change its behavior when its state changes (State).
