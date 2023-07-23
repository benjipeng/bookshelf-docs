---
bookCollapseSection: false
weight: 20
---

# Object Pool

The Object Pool pattern is a creational design pattern that uses a set of initialized objects kept ready to use, rather than allocating and destroying them on the fly. Here are the components of the Object Pool pattern:

## Component

1. **ObjectPool**: This is an interface that declares methods for acquiring and releasing objects.
2. **ConcreteObjectPool**: This is a class that implements the ObjectPool interface. It manages the object pool and implements the object pool management logic.
3. **PooledObject**: This is the type of object that the pool manages. It has a method for using the object.

### Relationship

- The `ConcreteObjectPool` class implements the `ObjectPool` interface and manages a pool of `PooledObject` instances.
- The `PooledObject` class represents the objects that are managed by the pool.

### Diagram

![Object-Pool-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/object-pool-pattern.svg)

## Java Implementation

```java
import java.util.concurrent.ConcurrentLinkedQueue;

// PooledObject
class PooledObject {
    public void use() {
        System.out.println("Using pooled object");
    }
}

// ObjectPool
interface ObjectPool {
    PooledObject acquire();
    void release(PooledObject pooledObject);
}

// ConcreteObjectPool
class ConcreteObjectPool implements ObjectPool {
    private ConcurrentLinkedQueue<PooledObject> pool = new ConcurrentLinkedQueue<>();

    public ConcreteObjectPool() {
        for (int i = 0; i < 10; i++) {
            pool.add(new PooledObject());
        }
    }

    @Override
    public PooledObject acquire() {
        return pool.poll();
    }

    @Override
    public void release(PooledObject pooledObject) {
        pool.add(pooledObject);
    }
}

// Main class
public class ObjectPoolPatternDemo {
    public static void main(String[] args) {
        ObjectPool objectPool = new ConcreteObjectPool();
        PooledObject pooledObject = objectPool.acquire();
        pooledObject.use();
        objectPool.release(pooledObject);
    }
}
```

- The `PooledObject` class represents the objects that are managed by the pool. It has a use method for using the object.
- The `ObjectPool` interface declares methods for acquiring and releasing `PooledObject` instances.
The `ConcreteObjectPool` class implements the ObjectPool interface. It manages a pool of `PooledObject` instances using a `ConcurrentLinkedQueue`. In its constructor, it initializes the pool with 10 `PooledObject` instances. The acquire method retrieves and removes a `PooledObject` from the pool, and the release method adds a `PooledObject` back to the pool.
- In the `ObjectPoolPatternDemo` class, we create a `ConcreteObjectPool`, acquire a `PooledObject` from the pool, use the `PooledObject`, and then release it back to the pool.

When you run the `ObjectPoolPatternDemo`, it will print "Using pooled object", indicating that a `PooledObject` has been acquired from the pool and used.

## Learn More

Singleton Pattern: The Singleton pattern ensures that a class has only one instance and provides a global point of access to it. The Singleton pattern is similar to the Object Pool pattern in that they both control the creation of objects. However, the Singleton pattern is used when we want to ensure that only one instance of a class exists, while the Object Pool pattern is used when we want to manage a pool of reusable objects.

Factory Method Pattern: The Factory Method pattern provides a way to delegate the instantiation logic to child classes. The Factory Method pattern is similar to the Object Pool pattern in that they both are used to create objects. However, the Factory Method pattern is used when we want to provide an extension point for derived classes, while the Object Pool pattern is used when we want to manage a pool of reusable objects.

Prototype Pattern: The Prototype pattern is used when the type of objects to create is determined by a prototypical instance, which is cloned to produce new objects. The Prototype pattern is similar to the Object Pool pattern in that they both are used to create objects. However, the Prototype pattern is used when we want to clone or copy existing objects, while the Object Pool pattern is used when we want to manage a pool of reusable objects.

```c
classDiagram
    ObjectPool <|.. ConcreteObjectPool
    ObjectPool <|.. PooledObject
    class ObjectPool{
        +acquire(): PooledObject
        +release(pooledObject: PooledObject)
    }
    class ConcreteObjectPool{
        +acquire(): PooledObject
        +release(pooledObject: PooledObject)
    }
    class PooledObject{
        +use()
    }
```
