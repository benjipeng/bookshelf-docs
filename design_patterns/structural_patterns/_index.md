---
bookCollapseSection: true
weight: 20
---

# An overview of Design Patterns in OOP

> Design patterns are **typical** solutions to common problems in software design. Each pattern is like a blueprint that you can customize to solve a particular design problem in your code. They are descriptions or templates for how to solve a problem that can be used in many different situations.

Design patterns are categorized into three types:

- `Creational Patterns:` Try to *create* objects in a manner suitable to the situation. *{deal with object creation mechanism}*
- `Structural Patterns:` Compose interfaces and define ways to compose objects to gain new functionality. *{class / object composition}*
- `Behavioral Patterns:` Algorithm and assignment of responsibilities between objects.

## A note on Java

> In Java, you can **only** have one public class per `.java` file, and the file name must match the name of the public class. However, you can have multiple non-public classes in the same `.java` file.

For the Bridge design pattern example, you would typically have a separate .java file for each class or interface. Here's how you might organize your files:

```lua
src/
|-- main/
|   |-- java/
|   |   |-- com/
|   |   |   |-- example/
|   |   |   |   |-- bridge/
|   |   |   |   |   |-- Device.java
|   |   |   |   |   |-- Radio.java
|   |   |   |   |   |-- Tv.java
|   |   |   |   |   |-- RemoteControl.java
|   |   |   |   |   |-- AdvancedRemoteControl.java
|   |   |   |   |   |-- Main.java
```

To compile and run the `Main` class from the command line, you would first navigate to the `src` directory, then use the `javac` command to compile the `.java` files into bytecode (`.class` files), and then use the java command to run the `Main` class. Here's how you can do it:

```bash
# Navigate to the src directory
cd src

# Compile the .java files
javac main/java/com/example/bridge/*.java

# Run the Main class
java main.java.com.example.bridge.Main
```
