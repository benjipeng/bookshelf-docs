# Basic Haskell

{{< hint danger >}}
Haskell is a purely functional, statically typed programming language with a strong focus on immutability, lazy evaluation, and type inference
{{< /hint >}}

## `main` Function

{{<hint warning>}}
In Haskell, the `main` function serves as the *entry point* for the program execution (*It is a top-level function that performs I/O and other side effects*). It has the type signature `IO ()` and is responsible for performing side effects, such as printing to the console, reading input, or working with files.
{{</hint>}}

>Here's a basic `main` function that prints "hello, world!" to the console:

```haskell
main :: IO()

main = putStrLn "hello, world!"
```

In this example, `putStrLn` is an I/O action that writes a string to the console followed by a newline. It has the type signature `String -> IO ()`.

>To perform multiple I/O actions in sequence, you can use the `do` notation. The `do` notation allows you to combine I/O actions into a single I/O action. Here's an example that demonstrates how to use the `do` notation in the main function:

```haskell
main :: IO ()
main = do
  putStrLn "What's your name?"
  name <- getLine
  putStrLn ("Hello, " ++ name ++ "!")
```

In this example, we use `getLine` to read a line of text from the console. `getLine` is an I/O action with the type signature IO String. The `<-` operator is used to bind the result of an I/O action to a variable. In this case, we bind the result of `getLine` to the variable name.

Please note that the `<-` operator can only be used within a `do` block. Also, the last action in a `do` block must have the type `IO ()`.

```haskell
add :: Int -> Int -> Int
add x y = x + y

main :: IO ()
main = do
  putStrLn "Enter the first number:"
  num1 <- readLn
  putStrLn "Enter the second number:"
  num2 <- readLn
  let sum = add num1 num2
  putStrLn ("The sum of the numbers is: " ++ show sum)
```

```haskell
-- main.hs
add :: Int -> Int -> Int
add x y = x + y

main :: IO ()
main = do
  let x = 1
  let y = 2
  putStrLn (show (add x y))
```

```shell
$ ghc -o program Main.hs
$ ./program
```
## Variable and Constants

> In Haskell, variables are **immutable** by default. You can define a variable using a simple assignment.

```haskell
variableName :: Type
variableName = value
-- Example:
answer :: Int
answer = 42
```
## Basic Data Types
Haskell has several built-in data types, such as Int, Integer, Float, Double, Char, and Bool.
```haskell
intVal :: Int
intVal = 42

floatVal :: Float
floatVal = 3.14

charVal :: Char
charVal = 'A'

boolVal :: Bool
boolVal = True
```

## Functions
> Functions in Haskell are defined using a simple assignment. The function name is followed by its parameters, and the function body is an expression.
haskell
```haskell
functionName :: Type1 -> Type2 -> ReturnType
functionName parameter1 parameter2 = expression
-- Example:
add :: Int -> Int -> Int
add x y = x + y
```
## Control Flow
> Haskell uses guards and pattern matching as control flow structures. Here's an example using guards
```haskell
-- Guard
absolute :: Int -> Int
absolute x
  | x >= 0    = x
  | otherwise = -x
-- Pattern Matching
factorial :: Integer -> Integer
factorial 0 = 1
factorial n = n * factorial (n - 1)
```