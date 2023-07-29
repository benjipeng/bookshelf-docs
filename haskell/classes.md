# Classes in Haskell

In Haskell, classes **define** a **type** that has certain operations defined for it. Classes have similarities with `interfaces` in languages like Java.

## Basic Examples

```haskell
class BasicClass a where
  method1 :: a -> a -> Bool
  method2 :: a -> a
```

> In the above snippet, `BasicClass` is a type class that accept a type `a`. It has two methods `method1` and `method2`, which have been defined but *not* implemented. ***To provide the implementation, we must create instances of the class***.

To create an instance of `BasicClass` for the type `Int`:

```haskell
instance BasicClass Int where
  method1 x y = x == y
  method x = x + 1
```

### More Than One Types

A type class can accept more than one type. These are often called ***multi-parameter type classes***.

```haskell
class Convertible a b where
  convert :: a -> b
```

In this `Convertible` class, there are two type parameters `a` and `b`. The `convert` function converts an instance of type `a` into another instance of type `b`.

The instance of the class can be:

```haskell
instance Convertible Int String where
-- The same `as convert x = show x`
-- Point-free style
  convert = show

instance Convertible Double Int where
  convert = floor
```

> In point-free style (or tacit programming), instead of explicitly mentioning arguments, we construct and manipulate functions directly. This often results in cleaner, more readable code.

To use this multi-parameter type class:

```haskell
main = do 
  print (convert (123 :: Int) :: String)
  print (convert (123.5 :: Double) :: Int)
```

#### Type-directed Overloading

> The ability to use type annotations to guide type inference and disambiguate function calls is indeed a feature of Haskell and other statically-typed languages with sophisticated type systems, such as Scala and Rust.

> This feature stems from the **Hindley-Milner** type system upon which Haskell's type system is based. **Hindley-Milner** type systems are known for their strong, static typing rules and powerful type inference capabilities.

Here is an example using "**type-directed return overloading**" or "**return-type overloading**". A `Readable` *type class* that mimics the behavior of the `Read` *type class* in a simplified way. The difference here will be that our `readValue` function's behavior will depend on the return type, *not* on the type of its argument.

`Readable.hs`:

```haskell
{-# LANGUAGE MultiParamTypeClasses, FlexibleInstances #-}

module Readable (Readable(..)) where

-- Define the type class
class Readable a where
  readValue :: String -> a

-- Instance for Int
instance Readable Int where
  readValue = read

-- Instance for Integer
instance Readable Integer where
  readValue = toInteger . length
```

`Main.hs`:

```haskell
import Readable

main :: IO ()
main = do
  putStrLn $ "Parsed Int: " ++ show (readValue "12345" :: Int)
  putStrLn $ "String length as Integer: " ++ show (readValue "12345" :: Integer)
```

> **Note:** `putStrLn ("Parsed Int: " ++ show (readValue "12345" :: Int))` is also valid.
> The module `Readable (Readable(..))` where declaration at the top of a Haskell file ***defines*** a **module** named `Readable`. The items in parentheses after the module name (Readable(..)) specify what the module exports.
