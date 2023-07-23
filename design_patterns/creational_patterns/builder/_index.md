---
bookCollapseSection: false
weight: 20
---

# Builder

The Builder pattern is a ***creational design pattern*** that lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code. Here are the components of the Builder pattern:

## Component

1. Director: This class defines the order in which to execute the building steps. It works with a builder object to construct a complex object.
2. Builder: This is an interface that specifies methods for creating the different parts of the Product objects.
3. ConcreteBuilder: This class provides the implementation for the Builder interface. It is an object able to construct other objects. Concrete builders implement these operations to create particular representations of the product.
4. Product: This is the complex object that is being built. Products are constructed by corresponding concrete builders.

### Relationship

- The `Director` class is configured with a `Builder` instance which it uses to build a Product.
- The `Builder` interface defines the building steps that the director can use.
- The `ConcreteBuilder` classes implement the building steps defined in the `Builder` interface.
- The `Product` is the complex object that is being built.

### Diagram

![builder-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/builder-pattern.svg)

## Java Implementation

```java
// Product
class Car {
    private String engine;
    private String wheels;
    private String color;

    public void setEngine(String engine) {
        this.engine = engine;
    }

    public void setWheels(String wheels) {
        this.wheels = wheels;
    }

    public void setColor(String color) {
        this.color = color;
    }
}

// Builder
interface CarBuilder {
    void buildEngine();
    void buildWheels();
    void buildColor();
    Car getCar();
}

// ConcreteBuilder
class SportsCarBuilder implements CarBuilder {
    private Car car;

    public SportsCarBuilder() {
        this.car = new Car();
    }

    public void buildEngine() {
        car.setEngine("Sports Engine");
    }

    public void buildWheels() {
        car.setWheels("Sports Wheels");
    }

    public void buildColor() {
        car.setColor("Red");
    }

    public Car getCar() {
        return this.car;
    }
}

// Director
class CarDirector {
    private CarBuilder builder;

    public CarDirector(CarBuilder builder) {
        this.builder = builder;
    }

    public void buildCar() {
        builder.buildEngine();
        builder.buildWheels();
        builder.buildColor();
    }

    public Car getCar() {
        return builder.getCar();
    }
}

// Main class
public class BuilderPatternDemo {
    public static void main(String[] args) {
        CarBuilder builder = new SportsCarBuilder();
        CarDirector director = new CarDirector(builder);
        director.buildCar();
        Car car = director.getCar();
    }
}
```

- The `Car` class represents the complex object that we are trying to build.
- The `CarBuilder` interface defines the steps to build a car.
- The `SportsCarBuilder` class is a concrete builder that implements the CarBuilder interface and provides the implementation for the steps to build a sports car.
- The `CarDirector` class is responsible for executing the building steps in a particular sequence to create a car.

When you run the BuilderPatternDemo, it will create a CarDirector object with a SportsCarBuilder, build a car, and then retrieve the car.

## Learn More

**Factory Method Pattern:** The Factory Method pattern provides a way to delegate the instantiation logic to child classes. The Factory Method pattern is similar to the Builder pattern in that they both are used to create objects. However, the Factory Method pattern is used when we want to provide an extension point for derived classes, while the Builder pattern is used when construction of a complex object should be independent of the parts that make up the object.

**Abstract Factory Pattern:** The Abstract Factory pattern provides an interface for creating families of related or dependent objects without specifying their concrete classes. The Abstract Factory pattern is similar to the Builder pattern in that they both abstract the object creation process. However, the Abstract Factory pattern is used when we want to return several related objects, while the Builder pattern is used to return one object.

**Prototype Pattern:** The Prototype pattern creates objects by cloning an existing object. This pattern is similar to the Builder pattern in that it also abstracts the process of object creation, but it does so in a way that allows for more flexibility in the types of objects that can be created.

### Mermaid Code

```c
classDiagram
    Director <|.. ConcreteDirector
    Builder <|.. ConcreteBuilder
    Product <|.. ConcreteProduct
    class Director{
        -builder: Builder
        +setBuilder(builder: Builder)
        +construct()
    }
    class ConcreteDirector{
        +construct()
    }
    class Builder{
        +buildPartA()
        +buildPartB()
        +getProduct(): Product
    }
    class ConcreteBuilder{
        +buildPartA()
        +buildPartB()
        +getProduct(): Product
    }
    class Product{
    }
    class ConcreteProduct{
    }
```
