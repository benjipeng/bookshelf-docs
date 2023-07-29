# Scala

{{< hint warning >}}
Scala is a statically typed, general-purpose programming language that combines functional and object-oriented programming. It runs on the Java Virtual Machine (JVM) and is fully interoperable with Java.
{{< /hint >}}

## Variables and Constants

To declare a mutable variable, use the var keyword, followed by the variable name, type, and value. For immutable variables, use the val keyword instead.

```scala
var variableName: Type = value
val constantName: Type = value
```

## Data Type

```scala
val integer: Int = 42
val double: Double = 3.14
val float: Float = 2.7f
val boolean: Boolean = true
val text: String = "Hello, world!"
```

## Control Flow

Scala offers standard control flow structures, such as *if*, *else*, *match*, *for*, and *while*.

```scala
// If-else statement
if (condition) {
    // Execute this code if the condition is true
} else {
    // Execute this code if the condition is false
}

// Match (similar to switch) statement
value match {
  case value1 => // Execute this code if the value matches value1
  case value2 => // Execute this code if the value matches value2
  case _ => // Execute this code if none of the cases match the value
}

// For loop
for (i <- 0 until 10) {
    // Execute this code 10 times, with i taking values from 0 to 9
}

// While loop
while (condition) {
    // Execute this code while the condition is true
}
```

## Function

Functions in Scala are defined with the def keyword, followed by the function name, parameter list, return type, and function body.

```scala
def functionName(parameter1: Type1, parameter2: Type2): ReturnType = {
    // Function body
    result
}
```

## Classes, Traits, and Objects

Scala supports object-oriented programming with classes, traits (similar to interfaces), and singleton objects.

```scala
// Class definition
class ClassName {
    // Properties and methods
}

// Trait definition
trait TraitName {
    // Abstract and concrete methods
}

// Object definition (singleton)
object ObjectName {
    // Properties and methods
}
```
