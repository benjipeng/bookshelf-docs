# Swift

{{< hint info >}}
Swift is a powerful, modern, and easy-to-learn programming language developed by Apple for iOS, macOS, watchOS, tvOS, and Linux platforms. It was designed to be both fast and efficient while maintaining a focus on safety and readability. Here is the outline of some basic syntax elements in Swift
{{< /hint >}}

## Basics

### 1. Variables and Constants

To declare a **variable**, use the `var` keyword, followed by the `variable name` and `type`. If you want to declare a **constant**, use the `let` keyword instead.

```swift
var variableName: Type = value
let constantName: Type = value
```

### 2. Data Types

Swift has several built-in data types, such as Int, Double, Float, Bool, and String. You can also create your own custom data types using structures, classes, and enumerations.

```swift
let integer: Int = 42
let double: Double = 3.14
let float: Float = 2.7
let boolean: Bool = true
let text: String = "Hello, world!"
```

### 3. Control Flow

Swift offers the standard control flow structures, such as if, else, switch, for, and while.

```swift
// If-else statement
if condition {
    // Execute this code if the condition is true
} else {
    // Execute this code if the condition is false
}

// Switch statement
switch value {
case value1:
    // Execute this code if the value matches value1
case value2:
    // Execute this code if the value matches value2
default:
    // Execute this code if none of the cases match the value
}

// For loop
for i in 0..<10 {
    // Execute this code 10 times, with i taking values from 0 to 9
}

// While loop
while condition {
    // Execute this code while the condition is true
}
```

### 4. Function

Functions in Swift are defined with the func keyword, followed by the function name, parameter list, return type, and function body.

```swift
func functionName(parameter1: Type1, parameter2: Type2) -> ReturnType {
    // Function body
    return result
}
```

### 5. Classes, Structures, and Enums

Swift supports object-oriented programming through classes, as well as value types through structures and enumerations.

```swift
// Class definition
class ClassName {
    // Properties and methods
}

// Structure definition
struct StructName {
    // Properties and methods
}

// Enumeration definition
enum EnumName {
    case case1
    case case2
    // Additional cases
}
```

### 6. Optionals

Swift uses optionals to represent the absence of a value. An optional is a type that can either hold a value or be nil.

```swift
var optionalVariable: Type? = nil // Declare an optional variable
optionalVariable = value // Assign a value to the optional variable

if let unwrappedValue = optionalVariable {
    // Use unwrappedValue if optionalVariable is not nil
}
```

These are just a few examples of Swift's syntax, which is designed to be clear, concise, and easy to read. There's a lot more to explore, but this should give you a good starting point.

## More

### 1. Tuples

Tuples allow you to group multiple values together into a single compound value. You can use tuples to return multiple values from a function or store related values together without creating a custom data type.

```swift
let coordinates: (Int, Int) = (x: 10, y: 20)
let (x, y) = coordinates
print("X: \(x), Y: \(y)") // Output: "X: 10, Y: 20"
```

### 2. Type Aliases

Type aliases allow you to create a new name for an existing type. This can make your code more readable and expressive.

```swift
typealias Velocity = (x: Double, y: Double)
let velocity: Velocity = (x: 5.0, y: -3.0)
```

### 3. Closures

Closures are self-contained, anonymous functions that capture and store references to variables and constants from the surrounding context.

```swift
let numbers = [3, 1, 6, 2, 8]
let sortedNumbers = numbers.sorted { (a: Int, b: Int) -> Bool in
    return a < b
}
```

### 4. Error Handling

Swift provides built-in support for throwing, catching, and propagating errors using throw, throws, try, catch, and defer.

```swift
enum NetworkError: Error {
    case invalidURL
    case noData
}

func fetchData(from url: String) throws -> Data {
    // If the URL is invalid, throw an error
    guard let url = URL(string: url) else {
        throw NetworkError.invalidURL
    }

    // If the data is not available, throw an error
    guard let data = try? Data(contentsOf: url) else {
        throw NetworkError.noData
    }

    return data
}

do {
    let data = try fetchData(from: "https://example.com/data")
    // Process the data
} catch {
    print("An error occurred: \(error)")
}
```

### 5. Extensions

Extensions allow you to add new functionality to an existing class, structure, enumeration, or protocol type.

```swift
extension Int {
    var isEven: Bool {
        return self % 2 == 0
    }
}

let number = 4
if number.isEven {
    print("The number is even.")
}
```

### 6. Protocols

Protocols define a blueprint of methods, properties, and other requirements that can be implemented by any class, structure, or enumeration type.

```swift
protocol Animal {
    var numberOfLegs: Int { get }
    func makeSound()
}

class Dog: Animal {
    var numberOfLegs: Int {
        return 4
    }

    func makeSound() {
        print("Woof!")
    }
}

let dog = Dog()
dog.makeSound() // Output: "Woof!"
```

### 7. Generics

Generics enable you to write flexible, reusable functions and types that can work with any type, subject to the requirements you define.

```swift
var x = 3
   var y = 5
   swapValues(a: &x, b: &y)
   print("x: \(x), y: \(y)") // Output: "x: 5, y: 3"

   var string1 = "Hello"
   var string2 = "World"
   swapValues(a: &string1, b: &string2)
   print("string1: \(string1), string2: \(string2)") // Output: "string1: World, string2: Hello"
```

```swift

protocol Container {
    associatedtype ItemType
    func add(item: ItemType)
    func count() -> Int
}

class Stack<T>: Container {
    private var items: [T] = []

    func add(item: T) {
        items.append(item)
    }

    func count() -> Int {
        return items.count
    }

    func pop() -> T? {
        return items.popLast()
    }
}

let intStack = Stack<Int>()
intStack.add(item: 1)
intStack.add(item: 2)
intStack.add(item: 3)
print(intStack.count()) // Output: 3
print(intStack.pop()) // Output: Optional(3)
```
