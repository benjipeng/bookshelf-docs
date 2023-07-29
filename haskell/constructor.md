# Constructors in Haskell

In haskell, you shall provide a **type constructor** and *one or more* **data constructors** when you define a datatype.

```haskell
{- File: Shape.hs
   `Shape` is a type constructor.
   `Circle` and `Rectangle` are data constructors.
-}
data Shape = Circle Float 
            | Rectangle Float Float
            deriving (Show)
```

- `Shape` is a type **constructor**, *NOT* a type itself. It is a `function` that *takes other types to produce a type at the type level*.
- `Circle` and `Rectangle` are data `constructors`. They are *effectively* functions that produce a value of the type `Shape`.

When defining a datatype in Haskell, the pattern is:

```haskell
data TypeName = DataConstructor1 Type1 Type2 | DataConstructor2 Type 3 | ... deriving Show
```

- `TypeName` defines the new type name
- `DataConstructor1`, `DataConstructor2`, etc. are data constructors. They are used to create values of the `TypeName` type. These data constructors can take parameters of other types (`Type1`, `Type2`, `Type3`, etc.) to create a value of the new type.
- The `|` symbol separates different data constructors within the same type definition.
- The `deriving` `Show` part automatically creates an instance of the `Show` type class for `TypeName`, enabling it to be represented as a string for printing.
