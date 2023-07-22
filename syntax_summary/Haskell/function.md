# Haskell Functions

{{<hint info>}}
Functions are the fundamental building blocks in Haskell, as it is a purely functional language. Functions in Haskell are defined using a simple assignment and have no side effects. Here's a more detailed look at functions in Haskell.
{{</hint>}}

## Type Signature
{{<hint danger>}}
In Haskell, a function's type signature provides information about the types of its input parameters and its return value. Type signatures are a powerful feature in Haskell because they help ensure correctness, enable better compiler optimizations, and improve code readability.
{{</hint>}}

A function type signature consists of the **function name**, followed by the `::` operator, and then the function's input and output types separated by `->`. The **last** type in the type signature is always the **return** type. Here's a basic example:
```haskell
add :: Int -> Int -> Int
add x y = x + y
```
> In this example, the `add` function takes two `Int` parameters and returns an `Int`. The type signature is `Int -> Int -> Int`.

### Type Variables
Type signatures can include `type variables`, which are **lowercase letters** representing **any** type. Type variables make functions ***polymorphic*** (i.e., they can work with multiple types). Here's an example of a polymorphic function:
```haskell
identity :: a -> a
identity x = x
```
### Typeclasses
**Typeclasses** can be used in type signatures to constrain the types of the type variables. **Typeclasses** are similar to ***interfaces*** in other languages, defining a set of functions that a type *must* implement. Here's an example that demonstrates the use of **typeclasses** in a type signature:
```haskell
equal :: Eq a => a -> a -> Bool
equal x y = x == y
```
> In this example, the `equal` function takes **two** parameters of the same type `a` and returns a `Bool`. The `Eq a` constraint in the type signature indicates that the type `a` must be an instance of the `Eq` typeclass. The type signature is `Eq a => a -> a -> Bool`. 
```haskell
combine :: (Monoid a, Show a) => a -> a -> String
combine x y = show (x <> y)
```
> In this example, the `combine` function takes two parameters of the same type `a` and returns a `String`. The `Monoid a` and `Show a` constraints in the type signature indicate that the type `a` must be an instance of both the `Monoid` and `Show` typeclasses. The type signature is `(Monoid a, Show a) => a -> a -> String`.

## Function Definition
> Functions are defined with a type signature, a name, parameters, and a body (expression). The type signature shows the input types and the return type of the function.
```haskell
functionName :: Type1 -> Type2 -> ... -> ReturnType
functionName parameter1 parameter2 ... = expression
-- Example:
add :: Int -> Int -> Int
add x y = x + y
```
## Function Application
> Functions in Haskell are applied using a space-separated syntax. The function name is followed by its arguments, separated by spaces.
```haskell
result = functionName arg1 arg2 ...
sum = add 3 4
```
## Function Composition
> In Haskell, you can compose functions using the `(.)` operator. Function composition is useful for creating new functions by chaining existing ones.
```haskell
 -- composedFunction = function1 . function2
square :: Int -> Int
square x = x * x

double :: Int -> Int
double x = x + x

squareThenDouble :: Int -> Int
squareThenDouble = double . square

result = squareThenDouble 3 -- 18
```

## Higher-order Functions
> Higher-order functions are functions that take other functions as arguments or return them as results. Type signatures for higher-order functions include function types as parameters or return values. Here's an example:
```haskell
applyTwice :: (a -> a) -> a -> a
applyTwice f x = f (f x)
```
In this example, the `applyTwice` function takes a function `f` of type `a -> a` and a value `x` of type `a`, then applies the function `f` **twice** to the value `x`. The type signature is `(a -> a) -> a -> a`.

