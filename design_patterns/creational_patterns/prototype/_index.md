---
bookCollapseSection: false
weight: 20
---

# Prototype

The `Prototype` pattern is a ***creational design pattern*** that lets you copy existing objects without making your code dependent on their classes. Here are the components of the Prototype pattern:

## Component

1. `Prototype`: This is an interface that declares a method for cloning itself.
2. `ConcretePrototype`: This is a class that implements the cloning method defined in the Prototype interface. It returns a copy of itself.

### Relationship

The `ConcretePrototype` class implements the `Prototype` *interface* and defines the clone method.

### Diagram

![Prototype-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/prototype-pattern.svg)

## Java Implementation

```java
// Prototype
public abstract class Prototype implements Cloneable {
    public abstract Prototype clone() throws CloneNotSupportedException;
}

// ConcretePrototype
public class ConcretePrototype extends Prototype {
    private String field;

    public ConcretePrototype(String field) {
        this.field = field;
    }

    public Prototype clone() throws CloneNotSupportedException {
        return new ConcretePrototype(field);
    }

    @Override
    public String toString() {
        return field;
    }
}

// Main class
public class PrototypePatternDemo {
    public static void main(String[] args) throws CloneNotSupportedException {
        ConcretePrototype original = new ConcretePrototype("Prototype");
        ConcretePrototype cloned = (ConcretePrototype) original.clone();

        System.out.println(original);
        System.out.println(cloned);
    }
}

```

- The `Prototype` class is an *abstract* class that declares a clone method.
- The `ConcretePrototype` class extends the `Prototype` class and *implements* the clone method. It returns a new `ConcretePrototype` object with the same field value as the current object.
- In the `PrototypePatternDemo` class, we create a `ConcretePrototype` object named original. We then clone this object to create a new object named cloned. The toString method is overridden to print the field value of the objects.

When you run the `PrototypePatternDemo`, it will print the field values of both the original and cloned objects, which will be the same.

## Learn More

1. **Factory Method Pattern**: The Factory Method pattern provides a way to delegate the instantiation logic to child classes. The Factory Method pattern is similar to the Prototype pattern in that they both are used to create objects. However, the Factory Method pattern is used when we want to provide an extension point for derived classes, while the Prototype pattern is used when we want to clone or copy existing objects.

2. **Abstract Factory Pattern**: The Abstract Factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes. The Abstract Factory pattern is similar to the Prototype pattern in that they both abstract the object creation process. However, the Abstract Factory pattern is used when we want to return several related objects, while the Prototype pattern is used to return a clone or copy of an existing object.

3. **Builder Pattern**: The Builder pattern is used to construct a complex object step by step and the final step will return the object. The process of constructing an object should be generic so that it can create different representations of the same object. The Builder pattern is similar to the Prototype pattern in that they both abstract the object creation process. However, the Builder pattern is used when construction of a complex object should be independent of the parts that make up the object, while the Prototype pattern is used to clone or copy existing objects.

### Mermaid Code

```c
classDiagram
    Prototype <|.. ConcretePrototype
    class Prototype{
        +clone(): Prototype
    }
    class ConcretePrototype{
        +clone(): Prototype
    }
```
