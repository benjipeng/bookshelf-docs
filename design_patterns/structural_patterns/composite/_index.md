---
bookCollapseSection: false
weight: 20
---

# Composite

The Composite pattern is a structural design pattern that lets you compose objects into **tree** structures and then work with these structures as if they were *individual* objects.

## Component

1. Component: This is the base class for all elements in the structure. It should declare common operations like `add`, `remove`, and `getChild`.
2. Leaf: This is a basic element of a tree that doesn't have sub-elements.
3. Composite: This is a container that can store other elements (both Composites and Leaves). It implements base Component operations and delegates the work to child Components.

### Relationship

- The Composite object uses the base Component interface to work with all objects in the composition structure.
- When the Composite's methods are called, it delegates the work to its child Components.

### Diagram

![Composite-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/composite-pattern.svg)

## Java Implementation

```java
import java.util.ArrayList;
import java.util.List;

// Component
interface Component {
    void operation();
}

// Leaf
class Leaf implements Component {
    private String name;

    public Leaf(String name) {
        this.name = name;
    }

    public void operation() {
        System.out.println("Leaf " + name + ": operation");
    }
}

// Composite
class Composite implements Component {
    private List<Component> children = new ArrayList<>();
    private String name;

    public Composite(String name) {
        this.name = name;
    }

    public void add(Component component) {
        children.add(component);
    }

    public void remove(Component component) {
        children.remove(component);
    }

    public void operation() {
        System.out.println("Composite " + name + ": operation");
        for (Component child : children) {
            child.operation();
        }
    }
}

// Main class
public class CompositePatternDemo {
    public static void main(String[] args) {
        Composite root = new Composite("root");
        root.add(new Leaf("Leaf A"));
        root.add(new Leaf("Leaf B"));

        Composite comp = new Composite("Composite X");
        comp.add(new Leaf("Leaf XA"));
        comp.add(new Leaf("Leaf XB"));

        root.add(comp);
        root.add(new Leaf("Leaf C"));

        Leaf leaf = new Leaf("Leaf D");
        root.add(leaf);
        root.remove(leaf);

        root.operation();
    }
}
```

- The Component interface defines a method operation() that encapsulates an operation.
- The Leaf class implements the Component interface. It represents a basic element of a tree that doesn't have sub-elements.
- The Composite class is a container that can store other elements (both Composites and Leaves). It implements the operation() method and delegates the work to its child Components.

When you run the CompositePatternDemo, it will create a tree structure with a root Composite that contains two Leaves and another Composite. The second Composite also contains two Leaves. The operation() method is then called on the root Composite, which calls the operation() method on each of its child Components.

## Learn More

1. Decorator Pattern: Like the Composite pattern, the Decorator pattern is also a structural design pattern that allows behavior to be added to an individual object, either statically or dynamically, without affecting the behavior of other objects from the same class. The main difference is that the Decorator pattern is used to add new functionality to an object, while the Composite pattern is used to add the same functionality to a group of objects.

2. Chain of Responsibility Pattern: The Chain of Responsibility pattern is a behavioral design pattern that lets you pass requests along a chain of handlers. Upon receiving a request, each handler decides either to process the request or to pass it to the next handler in the chain. It's similar to the Composite pattern in that it allows you to work with a tree-like structure of objects, but it's different in that it focuses on how the objects in the structure communicate with each other.

3. Flyweight Pattern: The Flyweight pattern is a structural design pattern that lets you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects, instead of keeping all of the data in each object. It's similar to the Composite pattern in that it deals with how objects are related and interact, but it's different in that it focuses on optimizing memory usage.

### Mermaid Code

```c
classDiagram
    Component <|.. Composite
    Component <|.. Leaf
    class Component{
        +operation()
        +add(component: Component)
        +remove(component: Component)
        +getChild(index: int): Component
    }
    class Composite{
        -children: List<Component>
        +operation()
        +add(component: Component)
        +remove(component: Component)
        +getChild(index: int): Component
    }
    class Leaf{
        +operation()
    }
```
