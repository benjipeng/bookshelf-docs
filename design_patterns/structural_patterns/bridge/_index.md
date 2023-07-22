---
bookCollapseSection: false
weight: 20
---

# Bridge design pattern

> The Bridge design pattern is a structural design pattern that decouples an abstraction from its implementation so that the two can vary independently. This pattern involves an interface acting as a bridge that makes the functionality of concrete classes independent from interface implementer classes.

Here is a `Mermaid` diagram

```c
classDiagram
    Device <|.. Radio
    Device <|.. Tv
    Device : +void turnOn()
    Device : +void turnOff()
    RemoteControl o-- Device
    RemoteControl : +void togglePower()
    AdvancedRemoteControl --|> RemoteControl
    AdvancedRemoteControl : +void mute()
```

```java
// Device.java
public interface Device {
    void turnOn();
    void turnOff();
}

// Radio.java
public class Radio implements Device {
    @Override
    public void turnOn() {
        System.out.println("Turning on the radio");
    }

    @Override
    public void turnOff() {
        System.out.println("Turning off the radio");
    }
}

// Tv.java
public class Tv implements Device {
    @Override
    public void turnOn() {
        System.out.println("Turning on the TV");
    }

    @Override
    public void turnOff() {
        System.out.println("Turning off the TV");
    }
}

// RemoteControl.java
public class RemoteControl {
    protected Device device;

    public RemoteControl(Device device) {
        this.device = device;
    }

    public void togglePower() {
        device.turnOn();
        device.turnOff();
    }
}

// AdvancedRemoteControl.java
public class AdvancedRemoteControl extends RemoteControl {
    public AdvancedRemoteControl(Device device) {
        super(device);
    }

    public void mute() {
        System.out.println("Muting the device");
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        RemoteControl radioRemote = new RemoteControl(new Radio());
        radioRemote.togglePower();

        AdvancedRemoteControl tvRemote = new AdvancedRemoteControl(new Tv());
        tvRemote.togglePower();
        tvRemote.mute();
    }
}
```

In the Bridge design pattern, the "bridge" is the link between the abstraction and its implementation. In this case, the RemoteControl class (and its subclass AdvancedRemoteControl) represents the abstraction, and the Device interface represents the implementation.

The "bridge" is the mechanism that allows the RemoteControl to control a Device without knowing the specifics of what kind of Device it is controlling. This is achieved through the Device interface, which provides a consistent way for RemoteControl to interact with different kinds of Device objects (like Radio or Tv).

So, in this context, the Device interface acts as the "bridge" between the RemoteControl abstraction and its implementation (Radio or Tv). The Device interface allows the RemoteControl to work with different Device implementations in a way that is decoupled from the specifics of those implementations. This is the essence of the Bridge design pattern.

## The diagram

> The Diagram is in `.SVG` format, it _MAY_ get oversized
> ![bridge](https://raw.githubusercontent.com/benjipeng/assets/main/rc/book/designpatterns/bridge-pattern.svg)
>
