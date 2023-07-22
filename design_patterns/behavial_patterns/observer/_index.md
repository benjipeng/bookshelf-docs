---
bookCollapseSection: false
weight: 20
---

# Observer

The Observer pattern is a *behavioral design pattern* that lets you define a subscription mechanism to notify multiple objects about any events that happen to the object they're observing.

The Observer pattern involves *two* types of classes:

- Subject: This is the object that has some interesting state or behavior that other objects want to keep track of. It maintains a list of observers and provides methods to add, remove, and notify them.
- Observer: This is an interface that defines the update() method, which observers must implement. The update() method is called by the subject when any changes occur.

```c
classDiagram
    Subject <|.. ConcreteSubject
    Subject : +void attach(Observer observer)
    Subject : +void detach(Observer observer)
    Subject : +void notifyObservers()
    ConcreteSubject : +void someBusinessLogic()
    Observer <|.. ConcreteObserver
    Observer : +void update(Subject subject)
    ConcreteObserver : +void update(Subject subject)
    ConcreteSubject o-- ConcreteObserver
```

![observer](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/observer-pattern.svg)

The `Subject` interface is implemented by the `ConcreteSubject` class. The `Observer` interface is implemented by the `ConcreteObserver` class. **The ConcreteSubject has an association with ConcreteObserver**.

```java
// Subject.java
import java.util.ArrayList;
import java.util.List;

public abstract class Subject {
    private List<Observer> observers = new ArrayList<>();

    public void attach(Observer observer) {
        observers.add(observer);
    }

    public void detach(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers() {
        for (Observer observer : observers) {
            observer.update(this);
        }
    }
}

// ConcreteSubject.java
public class ConcreteSubject extends Subject {
    private String state;

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
        this.notifyObservers();
    }
}

// Observer.java
public interface Observer {
    void update(Subject subject);
}

// ConcreteObserver.java
public class ConcreteObserver implements Observer {
    private String observerState;

    @Override
    public void update(Subject subject) {
        observerState = ((ConcreteSubject) subject).getState();
        System.out.println("Observer state updated to: " + observerState);
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        ConcreteSubject subject = new ConcreteSubject();
        ConcreteObserver observer1 = new ConcreteObserver();
        ConcreteObserver observer2 = new ConcreteObserver();

        subject.attach(observer1);
        subject.attach(observer2);

        subject.setState("New State");
    }
}
```

In this example, ConcreteObserver objects observer1 and observer2 are observing ConcreteSubject object subject. When the state of subject changes, it notifies observer1 and observer2, and they update their state accordingly.

The Observer pattern is similar to the Publish-Subscribe pattern. In fact, the Observer pattern is essentially a subset of the Publish-Subscribe pattern. The key difference is that in the Observer pattern, the Observers are aware of the Subject, whereas in the Publish-Subscribe pattern, publishers and subscribers don't need to know each other. This allows for greater flexibility and decoupling of the system components.
