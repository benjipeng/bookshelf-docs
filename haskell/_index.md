---
bookCollapseSection: true
weight: 20
---

# Haskell and Functional Programming

## Basic / Primitive Data Types

> Haskell has several basic or primitive data types. Here's a list of the most common ones:

1. **Int**: A fixed-precision integer type. For example: `5`, `10`, `-3`.
2. **Integer**: An *arbitrary-precision* integer type (i.e., it can be used to represent numbers of practically unlimited size at the cost of efficiency). For example: `123456789101112`.
3. **Float**: A single-precision floating point number. `3.14`.
4. **Double**: A double-precision floating point number. For example: 3.14159265.
5. **Bool**: A Boolean data type that can be either `True` or `False`.
6. **Char**: A character type represented as a single unicode character inside single quotes. For example: 'a', 'b', 'C'.
7. `[a]`: A list of values of the same type, denoted by square brackets around a list of elements separated by commas. For example: [1, 2, 3], ['a', 'b', 'c'].
8. `(a, b, ..., z)`: A tuple of values which can be of different types, denoted by parentheses around a list of elements separated by commas. For example: (1, 'a'), (True, 3.14, 'b', "Hello").

## Classes

In Haskell, a `class` is a type system construct that allows us to define a set of functions that must be implemented for a particular type. Here's an example of a simple class in Haskell:

```Haskell
class BasicEq a where
    isEqual :: a -> a -> Bool
```

The code above define the class `BasicEq` that consists one function `isEqual` which has a `type variable` -- `a` **is a type variable that will stand in for *whatever* the type to make an instance of** `BasicEq`.

To **create an instance** of `BasicEq` for a type, us the `instance` keyword. Here's how you might make `Bool` and instance of `BasicEq`:

```Haskell
instance BasicEq Bool where
    isEqual True True = True
    isEqual False False = True
    isEqual _     _ = False
```

A `class` can contain *multiple* functions, they can provide *default* implementations **for some functions in terms of others**.

`Equality.hs`

```Haskell
-- Define the Eq class
module Equality where
-- Define the Equality class
class Equality a where
  isEqual :: a -> a -> Bool
  isNotEqual :: a -> a -> Bool

  -- Default implementation for isNotEqual
  isNotEqual x y = not (isEqual x y)
```

`BoolEquality.hs`

```haskell
module BoolEquality where
import Equality
-- Define Bool as an instance of Equality
instance Equality Bool where
  isEqual True True   = True
  isEqual False False = True
  isEqual _ _         = False
```

```haskell
import Equality
import BoolEquality

main :: IO ()
main = do
  print $ isEqual True True    -- Outputs: True
  print $ isNotEqual True True -- Outputs: False
  print $ isEqual True False   -- Outputs: False
  print $ isNotEqual True False -- Outputs: True 
```
