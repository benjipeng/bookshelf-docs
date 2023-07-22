---
bookCollapseSection: false
weight: 20
---

# Bridge design pattern

> The Bridge design pattern is a structural design pattern that decouples an abstraction from its implementation so that the two can vary independently. This pattern involves an interface acting as a bridge that makes the functionality of concrete classes independent from interface implementer classes.

Here is a `Mermaid` diagram

```m
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
