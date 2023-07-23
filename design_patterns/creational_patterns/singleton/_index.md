---
bookCollapseSection: false
weight: 20
---

# Singleton

The Singleton pattern is a creational design pattern that lets you ensure that a class has only one instance, while providing a global access point to this instance. Here are the components of the Singleton pattern:

## Component

**Singleton:** This class defines the `getInstance` method that serves as an access point to the singleton instance. **This method returns the singleton instance**, and it's *static*, so it's accessible without creating an object of the class. The Singleton's `constructor` should always be *private* to prevent direct construction calls with the new operator.

### Relationship

The `Singleton` class is responsible for creating its own unique instance if it doesn't exist. It also provides a static method to access the instance.

### Diagram

![Singleton-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/singleton-pattern.svg)

## Java Implementation

```java
// Singleton
public class Singleton {
    private static Singleton instance;

    private Singleton() {
        // Private constructor to restrict instantiation of the class from other classes.
    }

    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

// Main class
public class SingletonPatternDemo {
    public static void main(String[] args) {
        Singleton singleton1 = Singleton.getInstance();
        Singleton singleton2 = Singleton.getInstance();

        System.out.println(singleton1 == singleton2);  // This will print 'true'
    }
}
```

> In this example:

- The `Singleton` class has a private constructor, so it cannot be instantiated from outside the class.
- The `getInstance` method checks if an instance of Singleton already exists. If not, it creates one and returns it. If an instance already exists, it simply returns that instance.

When you run the SingletonPatternDemo, it will create two Singleton objects (singleton1 and singleton2). However, both singleton1 and singleton2 will point to the same instance, so the comparison singleton1 == singleton2 will return true.

## Learn More

1. ***Factory Method Pattern***: The Factory Method pattern provides a way to delegate the instantiation logic to child classes. The Factory Method pattern is similar to the Singleton pattern in that they both are used to create objects. However, the Factory Method pattern is used when we want to provide an extension point for derived classes, while the Singleton pattern is used when we want to ensure that a class has only one instance.

2. ***Abstract Factory Pattern***: The Abstract Factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes. The Abstract Factory pattern is similar to the Singleton pattern in that they both abstract the object creation process. However, the Abstract Factory pattern is used when we want to return several related objects, while the Singleton pattern is used to return one object and ensure that a class has only one instance.

3. ***Builder Pattern***: The Builder pattern is used to construct a complex object step by step and the final step will return the object. The process of constructing an object should be generic so that it can create different representations of the same object. The Builder pattern is similar to the Singleton pattern in that they both abstract the object creation process. However, the Builder pattern is used when construction of a complex object should be independent of the parts that make up the object, while the Singleton pattern is used to ensure that a class has only one instance.

### Mermaid Code

```c
classDiagram
    Singleton <|.. Singleton
    class Singleton{
        -static instance: Singleton
        -Singleton()
        +static getInstance(): Singleton
    }
```
