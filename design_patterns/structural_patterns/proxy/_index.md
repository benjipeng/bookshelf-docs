---
bookCollapseSection: false
weight: 20
---

# Proxy

The Proxy pattern involves a class, called the proxy, that controls access to another class, called the real subject. The proxy and the real subject have the same interface, which allows a client to use a proxy just like it would use the real subject.

## Component

1. The Subject interface declares a request method.
2. The RealSubject class implements the Subject interface and provides the real functionality for the request method.
3. The Proxy class also implements the Subject interface. It has a reference to a RealSubject object and controls access to it. When a client makes a request through the proxy, the proxy forwards the request to the real subject.

### Diagram

![Proxy-Pattern](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/proxy-pattern.svg)

## Java Implementation

```java
// Subject interface
interface Subject {
    void request();
}

// RealSubject class
class RealSubject implements Subject {
    @Override
    public void request() {
        System.out.println("RealSubject: Handling request.");
    }
}

// Proxy class
class Proxy implements Subject {
    private RealSubject realSubject;

    public Proxy(RealSubject realSubject) {
        this.realSubject = realSubject;
    }

    @Override
    public void request() {
        System.out.println("Proxy: Checking access prior to firing a real request.");
        if (checkAccess()) {
            realSubject.request();
            logAccess();
        }
    }

    private boolean checkAccess() {
        // Some real checks should go here.
        System.out.println("Proxy: Checking access.");
        return true;
    }

    private void logAccess() {
        System.out.println("Proxy: Logging the time of request.");
    }
}

// Main class
public class ProxyPatternDemo {
    public static void main(String[] args) {
        RealSubject realSubject = new RealSubject();
        Subject proxy = new Proxy(realSubject);
        proxy.request();
    }
}
```

- The Subject *interface* declares a request method.
- The RealSubject class *implements* the Subject interface and provides the real functionality for the request method.
- The Proxy class also *implements* the Subject interface. It has a *reference* to a RealSubject object and controls access to it. When a client makes a request through the proxy, the proxy checks access, forwards the request to the real subject, and logs the access.

### Result

```bash
Proxy: Checking access prior to firing a real request.
Proxy: Checking access.
RealSubject: Handling request.
Proxy: Logging the time of request.
```

## Learn More

> Design patterns similar to the Proxy pattern include:

**Adapter Pattern:** The Adapter pattern converts the interface of a class into another interface that clients expect. The Adapter pattern is similar to the Proxy pattern in that they both provide a different interface to the real subject. However, the Adapter pattern is used when we want to make existing classes work with others without modifying their source code, while the Proxy pattern is used when we want to control access to the real subject.

**Decorator Pattern:** The Decorator pattern attaches new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors. The Decorator pattern is similar to the Proxy pattern in that they both have the same interface as the real subject and use composition to delegate requests to the real subject. However, the Decorator pattern is used when we want to add responsibilities to objects dynamically, while the Proxy pattern is used when we want to control access to the real subject.

**Facade Pattern:** The Facade pattern provides a simplified interface to a complex subsystem. The Facade pattern is similar to the Proxy pattern in that they both provide a different interface to the real subject. However, the Facade pattern is used when we want to hide the complexities of a subsystem and provide a simpler interface, while the Proxy pattern is used when we want to control access to the real subject.
