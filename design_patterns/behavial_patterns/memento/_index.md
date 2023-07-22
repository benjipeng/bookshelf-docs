---
bookCollapseSection: false
weight: 20
---

# Memento

The Memento pattern is a software design pattern that provides the ability to restore an object to its previous state (undo via rollback). The memento pattern is implemented with three objects: the originator, a caretaker, and a memento.

## Component

### Originator / Memento / Caretaker

- **Originator**: This is the object whose state needs to be saved and restored. It creates a memento object to save its state.
- **Memento**: This is an object having three members: state, getSavedState(), and setSavedState(state). It's used to store the state of the Originator. The class has two members: state and getState().
- **Caretaker**: The caretaker class sees and takes care of the memento but it cannot operate on it.

### Relationship

> The relationships between these components are as follows:

- The Originator creates a Memento and uses it to store its internal state.
- The Caretaker knows when to capture the Originator's state and when to restore it. It keeps track of the Memento but never operates on it.

### Diagram

#### Mermaid Code

```c
classDiagram
    Originator <|.. Memento
    Caretaker -- Memento
    class Originator{
        +createMemento()
        +restore(memento: Memento)
    }
    class Memento{
        -state
        +getState()
    }
    class Caretaker{
        +addMemento(memento: Memento)
        +getMemento(index: int): Memento
    }
```

![memento](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/memento-pattern.svg)

## Java Implementation

```java
// Memento class
class Memento {
    private String state;

    public Memento(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }
}

// Originator class
class Originator {
    private String state;

    public void setState(String state) {
        this.state = state;
    }

    public String getState() {
        return state;
    }

    public Memento saveStateToMemento() {
        return new Memento(state);
    }

    public void getStateFromMemento(Memento memento) {
        state = memento.getState();
    }
}

// Caretaker class
class Caretaker {
    private List<Memento> mementoList = new ArrayList<Memento>();

    public void add(Memento state) {
        mementoList.add(state);
    }

    public Memento get(int index) {
        return mementoList.get(index);
    }
}

// Main class
public class MementoPatternDemo {
    public static void main(String[] args) {
        Originator originator = new Originator();
        Caretaker caretaker = new Caretaker();

        originator.setState("State #1");
        caretaker.add(originator.saveStateToMemento());

        originator.setState("State #2");
        caretaker.add(originator.saveStateToMemento());

        originator.setState("State #3");
        caretaker.add(originator.saveStateToMemento());

        System.out.println("Current State: " + originator.getState());
        originator.getStateFromMemento(caretaker.get(0));
        System.out.println("First saved State: " + originator.getState());
        originator.getStateFromMemento(caretaker.get(1));
        System.out.println("Second saved State: " + originator.getState());
    }
}
```

> In this example:

1. The Memento `class` is used to **store the state of the** `Originator`.
2. The `Originator` creates a *NEW* `Memento` object whenever it needs to save its state. It can *ALSO* restore its state from a Memento.
3. The `Caretaker` class is used to *store* and *restore* the `Originator`'s state from the `Memento`. It ***holds*** the `Memento` but ***never*** modifies it.
4. When you run the `MementoPatternDemo`, it will *change* the state of the `Originator` and save each state to the `Caretaker`. It then prints the current state and the first and second saved states.

## Learn More

Design patterns similar to the Memento pattern include:

- **Command Pattern:** Like the Memento pattern, the Command pattern can also keep track of actions and allow undo operations. However, the Command pattern encapsulates a request as an object, thereby letting you parameterize other objects with different requests, queue or log requests, and support undoable operations.

- **State Pattern:** The State pattern allows an object to alter its behavior when its internal state changes. However, unlike the Memento pattern, the State pattern doesn't remember its previous states.

- **Snapshot Pattern:** The Snapshot pattern is a versioning pattern which is a variant of the Memento pattern. It provides a way to save a snapshot of an object's state so that it can be restored if needed. The difference is that the Snapshot pattern typically involves taking a snapshot of the entire system or subsystem, not just a single object.
