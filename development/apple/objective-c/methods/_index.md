---
bookCollapseSection: true
weight: 20
---
# Methods in Objective-C

{{< hint danger >}}
Objective-C methods are the building blocks of `classes` and `objects`. They define the behavior and functionality of an object. Here's a detailed explanation of Objective-C methods along with *multiple* examples:
{{< /hint >}}

## Instance and Class Methods

Objective-C has two types of methods: instance methods and class methods. Instance methods are denoted by a `'-'` sign and can be called on instances (objects) of a class. Class methods are denoted by a `'+'` sign and can be called on the class itself.

Objective-C methods are the building blocks of classes and objects. They define the behavior and functionality of an object. Here's a detailed explanation of Objective-C methods along with multiple examples:

Instance Method:

```objc
- (void)instanceMethod;
```

Class Method:

```objc
+ (void)classMethod;
```

## Method Declaration and Implementation

Methods are typically declared in the header (.h) file and implemented in the implementation (.m) file.

ExampleClass.h (Declaration):

```objc
@interface ExampleClass : NSObject
- (NSString *)greetPerson:(NSString *)name;
@end
```

ExampleClass.m (Implementation):

```objc
#import "ExampleClass.h"

@implementation ExampleClass
- (NSString *)greetPerson:(NSString *)name {
    return [NSString stringWithFormat:@"Hello, %@!", name];
}
@end
```

## Return Type and Parameters

The return type is specified in parentheses before the method name. Parameters are specified by a combination of data type, parameter name, and the parameter's local variable name. Multiple parameters are separated by colons.

Example:

```objc
- (int)addNumber:(int)num1 toNumber:(int)num2;
```

## Method Call

Methods are called using the square bracket notation. The object or class is placed inside the square brackets, followed by the method name and its parameters.

Instance Method Call:

```objc
ExampleClass *exampleObject = [[ExampleClass alloc] init];
NSString *greeting = [exampleObject greetPerson:@"John"];
```

Class Method Call:

```objc
[ExampleClass classMethod];
```

## Detailed Examples

### Method with multiple parameters and return type

Header file (`ExampleClass.h`):

```objc
@interface ExampleClass : NSObject
- (int)addNumber:(int)num1 toNumber:(int)num2;
@end
```

Implementation file (`ExampleClass.m`):

```objc
#import "ExampleClass.h"

@implementation ExampleClass
- (int)addNumber:(int)num1 toNumber:(int)num2 {
    return num1 + num2;
}
@end
```

Calling the method:

```objc
ExampleClass *exampleObject = [[ExampleClass alloc] init];
int result = [exampleObject addNumber:3 toNumber:5];
```

### Method without parameters and return type

Header file (ExampleClass.h):

```objc
@interface ExampleClass : NSObject
- (void)printHelloWorld;
@end
```

Implementation file (ExampleClass.m):

```objc
#import "ExampleClass.h"

@implementation ExampleClass
- (void)printHelloWorld {
    NSLog(@"Hello, World!");
}
@end
```

Calling the method:

```objc
ExampleClass *exampleObject = [[ExampleClass alloc] init];
[exampleObject printHelloWorld];
```

### Method with a class method

Header file (ExampleClass.h):

```objc
@interface ExampleClass : NSObject
+ (instancetype)exampleClassWithInitialValue:(int)value;
@end
```

Implementation file (ExampleClass.m):

```objc
#import "ExampleClass.h"

@implementation ExampleClass
+ (instancetype)exampleClassWithInitialValue:(int)value {
    ExampleClass *instance = [[ExampleClass alloc] init];
    // Perform some setup with the initial value
    return instance;
}
@end
```

Calling the method:

```objc
ExampleClass *exampleObject = [ExampleClass exampleClassWithInitialValue:42];
```

In this example, we have a ***class*** method that takes an *integer* parameter and returns an *instance* of the `ExampleClass` with some initial setup based on the passed value. The method is called directly on the `ExampleClass`, and the result is stored in the exampleObject variable.

## More on Methods

### Method Naming Conventions

Objective-C methods are named using a `self-descriptive` and `easy-to-understand` format. Method names should *describe* the *action* performed and the parameters involved.

Example:

```objc
- (float)multiplyNumber:(float)num1 byNumber:(float)num2;
```

This method name **clearly** explains that it multiplies two numbers.

### Using Methods with Blocks

`Blocks` are a powerful feature in Objective-C that allows you to define chunks of code as `"first-class"` objects. You can pass them as arguments to methods and return them from methods.

Example of a method that accepts a block as a parameter:

Header file (`ExampleClass.h`):

```objc
@interface ExampleClass : NSObject
- (void)performActionWithCompletion:(void (^)(BOOL success))completion;
@end
```

Implementation file (`ExampleClass.m`):

```objc
#import "ExampleClass.h"

@implementation ExampleClass
- (void)performActionWithCompletion:(void (^)(BOOL success))completion {
    // Perform some action
    
    // Call the completion block when the action is complete
    completion(YES);
}
@end
```

Calling the method:

```objc
ExampleClass *exampleObject = [[ExampleClass alloc] init];
[exampleObject performActionWithCompletion:^(BOOL success) {
    if (success) {
        NSLog(@"Action completed successfully.");
    } else {
        NSLog(@"Action failed.");
    }
}];
```

### Methods with Out Parameters

In Objective-C, you can use pointers to return values from a method through its parameters. This is useful when you need to return multiple values or when you need to indicate success or failure of a method.

Example:

Header file (ExampleClass.h):

```objc
@interface ExampleClass : NSObject
- (BOOL)divideNumber:(float)numerator byNumber:(float)denominator result:(float *)result;
@end
```

Implementation file (ExampleClass.m):

```objc
#import "ExampleClass.h"

@implementation ExampleClass
- (BOOL)divideNumber:(float)numerator byNumber:(float)denominator result:(float *)result {
    if (denominator == 0) {
        return NO;
    }
    
    *result = numerator / denominator;
    return YES;
}
@end
```

Calling the method:

```objc
ExampleClass *exampleObject = [[ExampleClass alloc] init];
float divisionResult;
BOOL success = [exampleObject divideNumber:10 byNumber:2 result:&divisionResult];

if (success) {
    NSLog(@"Result: %f", divisionResult);
} else {
    NSLog(@"Division by zero is not allowed.");
}
```

### Method Overloading

Objective-C does not support traditional method overloading like some other programming languages. However, you can achieve similar functionality by *using different method names* or using *default* values for parameters.

Example:

Header file (ExampleClass.h):

```objc
@interface ExampleClass : NSObject
- (void)performTask;
- (void)performTaskWithCount:(int)count;
@end
```

Implementation file (ExampleClass.m):

```objc
#import "ExampleClass.h"

@implementation ExampleClass
- (void)performTask {
    [self performTaskWithCount:1];
}

- (void)performTaskWithCount:(int)count {
    for (int i = 0; i < count; i++) {
        // Perform the task
    }
}
@end
```

Calling the methods:

```objc
ExampleClass *exampleObject = [[ExampleClass alloc] init];
[exampleObject performTask];
[exampleObject performTaskWithCount:5];
```

### Inheritance and Method Overriding

Objective-C supports inheritance, allowing a subclass to inherit methods and properties from its superclass. A subclass can override a method to provide its own implementation.

Example:

Header file (`BaseClass.h`):

```objc
@interface BaseClass : NSObject
- (void)printMessage;
@end
```

Implementation file (`BaseClass.m`):

```objc
#import "BaseClass.h"

@implementation BaseClass
- (void)printMessage {
    NSLog(@"Message from BaseClass.");
}
@end
```

Header file (`SubClass.h`):

```objc
#import "BaseClass.h"

@interface SubClass : BaseClass
- (void)printMessage;
@end
```

Implementation file (`SubClass.m`):

```objc
#import "SubClass.h"

@implementation SubClass
- (void)printMessage {
    NSLog(@"Message from SubClass.");
}
@end
```

Calling the methods:

```objc
BaseClass *baseObject = [[BaseClass alloc] init];
[baseObject printMessage];

SubClass *subObject = [[SubClass alloc] init];
[subObject printMessage];
```

### Categories

Categories in Objective-C allow you to ***add methods to an existing class*** *without* ***subclassing*** it. This is useful for **extending** a class's functionality or for **organizing** related methods.

Example:

Header file (`NSString+Greeting.h`):

```objc
#import <Foundation/Foundation.h>

@interface NSString (Greeting)
- (NSString *)greetWithName;
@end
```

Implementation file (`NSString+Greeting.m`):

```objc
#import "NSString+Greeting.h"

@implementation NSString (Greeting)
- (NSString *)greetWithName {
    return [NSString stringWithFormat:@"Hello, %@!", self];
}
@end
```

Using the category method:

```objc
#import "NSString+Greeting.h"

NSString *name = @"John";
NSString *greeting = [name greetWithName];
NSLog(@"%@", greeting);
```

### Protocols

Protocols in Objective-C define a set of methods that a class can adopt and implement. They are used to create contracts that classes can conform to, enabling a form of multiple inheritance.

Example:

Header file (Printable.h):

```objc
@protocol Printable <NSObject>
- (void)print;
@end
```

Header file (Document.h):

```objc
#import "Printable.h"

@interface Document : NSObject <Printable>
@end
```

Implementation file (Document.m):

```objc
#import "Document.h"

@implementation Document
- (void)print {
    NSLog(@"Printing document...");
}
@end
```

Using a protocol method:

```objc
Document *doc = [[Document alloc] init];
[doc print];
```
