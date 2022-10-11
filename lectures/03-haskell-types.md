---
title: Algebraic Data Types
headerImg: sea.jpg
---

## Recap: Haskell Crash Course

![](/static/img/trinity.png){#fig:types .align-center width=60%}

- Core program element is an **expression**
- Every _valid_ expression has a **type** (determined at compile-time)
- Every _valid_ expression reduces to a _value_ (computed at run-time)

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>    
    
    
## Representing complex data

**We've seen:**

  * *base* types: `Bool`, `Int`, `Integer`, `Float`
  * some ways to *build up* types: given types `T1, T2`
  
    - functions: `T1 -> T2`
    - tuples: `(T1, T2)`
    - lists: `[T1]`
    
<br>
<br>    
  
**Algebraic Data Types:** a single, powerful technique 
for building up types to represent complex data

  * lets you define your own data types
  * subsumes tuples and lists!
    
<br>
<br>
<br>
<br>
<br>
<br>

## Algebraic Data Types

1. ***Type Synonyms:* naming existing types**

2. *Product Types:* bundling things together

3. *Sum Types:* types with multiple variants

4. *Recursive Types:* types that contain themselves

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Type Synonyms

Synonyms are just names ("aliases") for existing types

- think `typedef` in `C`

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## A type to represent circles

A tuple `(x, y, r)` is a *circle* with center at `(x, y)` and radius `r`

```haskell
type CircleT = (Double, Double, Double)
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## A type to represent cuboids

A tuple `(length, depth, height)` is a *cuboid*

```haskell
type CuboidT = (Double, Double, Double)
```

![](https://upload.wikimedia.org/wikipedia/commons/d/dc/Cuboid.png){#fig:cuboid .align-center width=60%}


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Using Type Synonyms

We can now use synonyms by creating values of the given types

```haskell
circ0 :: CircleT 
circ0 = (0, 0, 100)  -- ^ circle at "origin" with radius 100

cub0 :: CuboidT
cub0 = (10, 20, 30)  -- ^ cuboid with l=10, d=20, h=30 
```

And we can write functions over synonyms too

```haskell
area :: CircleT -> Double
area (x, y, r) = pi * r * r  

volume :: CuboidT -> Double
volume (l, d, h) = l * d * h 
```

We should get this behavior

```haskell
>>> area circ0 
31415.926535897932

>>> volume cub0
6000
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## QUIZ 

Suppose we have the definitions

```haskell
type CircleT = (Double, Double, Double)
type CuboidT = (Double, Double, Double)

circ0 :: CircleT
circ0 = (0, 0, 100)  -- ^ circle at "origin" with radius 100

cub0 :: CuboidT
cub0 = (10, 20, 30)  -- ^ cuboid with length=10, depth=20, height=30 

area :: CircleT -> Double
area (x, y, r) = pi * r * r  

volume :: CuboidT -> Double
volume (l, d, h) = l * d * h
```

What is the result of

```haskell
>>> volume circ0
```

**A.** `0`

**B.** Type error

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Beware!

Type Synonyms 

* Do not _create_ new types

* Just _name_ existing types

And hence, synonyms 

* Do not prevent _confusing_ different values 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Algebraic Data Types

1. *Type Synonyms:* naming existing types \[done\]

2. ***Product Types:* bundling things together**

3. *Sum Types:* types with multiple variants

4. *Recursive Types:* types that contain themselves

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## Creating *New* Data Types 

We can avoid mixing up by creating _new_ `data` types

```haskell
-- | A new type `Circle` with constructor `MkCircle`,
--   which takes three arguments of type `Double`
data Circle = MkCircle Double Double Double

-- | A new type `Cuboid` with constructor `MkCuboid`
--   which takes three arguments of type `Double`
data Cuboid = MkCuboid Double Double Double
```

We use constructors to *build* values of the new type: 

```haskell
circ1 :: CircleT 
circ1 = MkCircle 0 0 100  -- ^ circle at "origin" w/ radius 100

cub1 :: Cuboid
cub1 = MkCuboid 10 20 30  -- ^ cuboid w/ len=10, dep=20, ht=30 
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## QUIZ

Suppose we create a new type with a `data` definition

```haskell
-- | A new type `CircleT` with constructor `MkCircle`
data Circle = MkCircle Double Double Double
```

What is the **type of** the `MkCircle` _constructor_?

**A.** `MkCircle :: CircleT`

**B.** `MkCircle :: Double -> CircleT`

**C.** `MkCircle :: Double -> Double -> CircleT`

**D.** `MkCircle :: Double -> Double -> Double -> CircleT`

**E.** `MkCircle :: (Double, Double, Double) -> CircleT`

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


### Aside: Record syntax

Haskell's **record syntax** allows you to *name* the constructor parameters:

  * Instead of

    ```haskell
    data Circle = MkCircle Double Double Double
    ```

  * you can write:

    ```
    data Circle = MkCircle { 
      center_x :: Double, 
      center_y :: Double,
      radius   :: Double  
    }
    ```
    
  * then you can do:
  
    ```
    circ1 = MkCircle { center_x = 0, center_y = 0, radius = 100 }
    -- same as: circ1 = MkCircle 0 0 100
    
    r = radius circ1 -- use field name as a function    
    ```


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## QUIZ 

Suppose we have the definitions

```haskell
type CuboidT = (Double, Double, Double)
data Cuboid  = MkCuboid Double Double Double     

volume :: CuboidT -> Double
volume (l, d, h) = l * d * h
```

What is the result of

```haskell
>>> volume (MkCuboid 10 20 30)
```

**A.** `6000`

**B.** Type error

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Deconstructing Data

Constructors let us *build* values of new type ... but how to *use* those values?

How can we implement a function

```haskell
volume :: Cuboid -> Double
volume c = ???
```

such that

```haskell
>>> volume (MkCuboid 10 20 30)
6000
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## Deconstructing Data by Pattern Matching

Haskell lets us *deconstruct* data via pattern-matching

```haskell
volume :: Cuboid -> Double
volume (MkCuboid l d h) = l * d * h

area :: Circle -> Double
area (MkCircle x y r) = pi * r * r
```

same as for tuples, just using different constructors!

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Algebraic Data Types

1. *Type Synonyms:* naming existing types \[done\]

2. *Product Types:* bundling things together \[done\]

3. ***Sum Types:* types with multiple variants**

4. *Recursive Types:* types that contain themselves

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

Defining new types with `data` prevents us from mixing up values:

```haskell
area :: Circle -> Double
area (MkCircle x y r) = pi * r * r

>>> area (MkCuboid 10 20 30) -- TYPE ERROR!
```

But ... what if we _need_ to mix up values?

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## A List of Shapes

Suppose I need to represent a *list of shapes*

- Some `Circle`s
- Some `Cuboid`s

What is the problem with `shapes` as defined below?

```haskell
shapes = [circ1, cub1]
```

Where we have defined

```haskell
circ1 :: Circle 
circ1 = MkCircle 0 0 100  -- ^ circle at "origin" with radius 100

cub1 :: Cuboid
cub1 = MkCuboid 10 20 30  -- ^ cuboid with length=10, depth=20, height=30 
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

This does not type-check!

All list elements must have the _same_ type!

<br>
<br>
<br>
<br>

Solution?

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Sum types

Lets create a _single_ type that can represent _both_ kinds of shapes!

```haskell
data Shape 
  = MkCircle Double Double Double   -- ^ Circle at x, y with radius r 
  | MkCuboid Double Double Double   -- ^ Cuboid with length, depth, height
```

A **sum type** is a data type with multiple constructors

  - aka **enum** in Rust
  - aka (tagged) **union** in C

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## QUIZ

With the definition:

```haskell
data Shape 
  = MkCircle Double Double Double   -- ^ Circle at x, y with radius r 
  | MkCuboid Double Double Double   -- ^ Cuboid with length, depth, height
```

What is the type of `MkCircle 0 0 100` ? 

**A.** `Shape`

**B.** `Circle`

**C.** `MkCircle`

**D.** `(Double, Double, Double)`

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## List of Shapes: Take 2

Now we can define

```haskell
circ2 :: Shape
circ2 = MkCircle 0 0 100  -- ^ circle at "origin" with radius 100

cub2 :: Shape 
cub2 = MkCuboid 10 20 30  -- ^ cuboid with length=10, depth=20, height=30 
```

and then define collections of `Shape`s

```haskell
shapes :: [Shape]
shapes = [circ1, cub1]
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## 2D Shapes 

Lets define a type for 2D shapes

```haskell
data Shape2D 
  = MkRect Double Double -- ^ 'MkRect w h' is a rectangle with width 'w', height 'h'
  | MkCirc Double        -- ^ 'MkCirc r' is a circle with radius 'r'
  | MkPoly [Vertex]      -- ^ 'MkPoly [v1,...,vn]' is a polygon with vertices at 'v1...vn'

type Vertex = (Double, Double)
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Tagged Boxes 

Values of this type are either two doubles *tagged* with `Rectangle` 

```haskell
>>> :type (Rectangle 4.5 1.2)
(Rectangle 4.5 1.2) :: Shape
```

or a list of pairs of `Double` values *tagged* with `Polygon`

```haskell
ghci> :type (Polygon [(1, 1), (2, 2), (3, 3)])
(Polygon [(1, 1), (2, 2), (3, 3)]) :: Shape
```

<br>
<br>
<br>

Data values inside special **Tagged Boxes**

![Datatypes are Boxed-and-Tagged Values](/static/img/lec4_boxed.png)


<br>
<br>
<br>
<br>

How do we get the value out of the box?

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## EXERCISE 

Write a function to compute the `perimeter` of a `Shape2D` 

```haskell
perimeter :: Shape2D -> Double
perimeter s = ???
```

**HINT**

You may want to use this helper that computes the distance between two points

```haskell
distance :: Vertex -> Vertex -> Double
distance (x1, y1) (x2, y2) = sqrt ((x2 - x1) ** 2 + (y2 - y1) ** 2)
```

<br>
<br>
<br>
<br>
<br>
<br>

## Algebraic Data Types

1. *Type Synonyms:* naming existing types \[done\]

2. *Product Types:* bundling things together \[done\]

3. *Sum Types:* types with multiple variants  \[done\]

4. ***Recursive Types:* types that contain themselves**


<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## *Recursive* Data Types

We can define datatypes *recursively* too

```haskell
data IntList 
  = INil                -- ^ empty list
  | ICons Int IntList   -- ^ list with "hd" Int and "tl" IntList
  deriving (Show)
```

(Ignore the bit about `deriving` for now.) 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## QUIZ 

```haskell
data IntList 
  = INil                -- ^ empty list
  | ICons Int IntList   -- ^ list with "hd" Int and "tl" IntList
  deriving (Show)
```

What is the type of `ICons` ?

**A.** `Int -> IntList -> List`

**B.** `IntList`

**C.** `Int -> IntList -> IntList`

**D.** `Int -> List    -> IntList`

**E.** `IntList -> IntList`

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## Constructing `IntList`

Can *only* build `IntList` via constructors.

```haskell
>>> :type INil 
INil:: IntList

>>> :type ICons
ICons :: Int -> IntList -> IntList
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## EXERCISE 

Write down a representation of type `IntList` of the list of three numbers `1`, `2` and `3`.

```haskell
list_1_2_3 :: IntList
list_1_2_3 = ???
```

**Hint** Recursion means boxes *within* boxes

![Recursively Nested Boxes](/static/img/lec4_nested.png)

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Trees: Multiple Recursive Occurrences

We can represent `Int` *trees* like 

```haskell
data IntTree 
   = ILeaf Int              -- ^ single "leaf" w/ an Int
   | INode IntTree IntTree  -- ^ internal "node" w/ 2 sub-trees
   deriving (Show)
```

A *leaf* is a box containing an `Int` tagged `ILeaf` e.g.

```haskell
>>> it1  = ILeaf 1 
>>> it2  = ILeaf 2
```

A *node* is a box containing two sub-trees tagged `INode` e.g. 

```haskell
>>> itt   = INode (ILeaf 1) (ILeaf 2)
>>> itt'  = INode itt itt
>>> INode itt' itt'
INode (INode (ILeaf 1) (ILeaf 2)) (INode (ILeaf 1) (ILeaf 2))
``` 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Multiple Branching Factors

e.g. [2-3 trees](http://en.wikipedia.org/wiki/2-3_tree) 

```haskell
data Int23T 
  = ILeaf0 
  | INode2 Int Int23T Int23T
  | INode3 Int Int23T Int23T Int23T
  deriving (Show)
```

An example value of type `Int23T` would be

```haskell
i23t :: Int23T
i23t = INode3 0 t t t
  where t = INode2 1 ILeaf0 ILeaf0
```

which looks like 

![Integer 2-3 Tree](/static/img/lec4_int23t.png)

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Parameterized Types

We can define `CharList` or `DoubleList` 
- versions of `IntList` for `Char` and `Double` as

```haskell
data CharList 
  = CNil
  | CCons Char CharList
  deriving (Show)

data DoubleList 
   = DNil
   | DCons Char DoubleList
   deriving (Show)
``` 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Don't Repeat Yourself!

Don't repeat definitions 
- Instead *reuse* the list *structure* across *all* types!

Find abstract *data* patterns by 

- identifying the *different* parts and 
- refactor those into *parameters* 

<br>
<br>
<br>
<br>
<br>
<br>
<br>

## A Refactored List

Here are the three types: What is common? What is different?

```haskell
data IList = INil | ICons Int    IList

data CList = CNil | CCons Char   CList

data DList = DNil | DCons Double DList
``` 

**Common:** `Nil`/`Cons` structure

**Different:** type of each "head" element

### Refactored using Type Parameter

```haskell
data List a = Nil | Cons a  (List a)
```

### Recover original types as *instances* of `List`

```haskell
type IntList    = List Int
type CharList   = List Char
type DoubleList = List Double
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Polymorphic Data has Polymorphic Constructors

Look at the types of the constructors 

```haskell
>>> :type Nil 
Nil :: List a
```

That is, the `Empty` tag is a value of *any* kind of list, and

```haskell
>>> :type Cons 
Cons :: a -> List a -> List a
```

`Cons` takes an `a` *and* a `List a` and returns a `List a`.

```haskell
cList :: List Char     -- list where 'a' = 'Char' 
cList = Cons 'a' (Cons 'b' (Cons 'c' Nil))

iList :: List Int      -- list where 'a' = 'Int' 
iList = Cons 1 (Cons 2 (Cons 3 Nil))

dList :: List Double   -- list where 'a' = 'Double' 
dList = Cons 1.1 (Cons 2.2 (Cons 3.3 Nil))
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Polymorphic Function over Polymorphic Data

Lets write the list length function

```haskell
len :: List a -> Int
len Nil         = 0
len (Cons x xs) = 1 + len xs
``` 

`len` doesn't care about the actual *values* in the list
- only "counts" the number of `Cons` constructors 

Hence `len :: List a -> Int` 

- we can call `len` on **any kind of list**. 

```haskell
>>> len [1.1, 2.2, 3.3, 4.4]    -- a := Double  
4

>>> len "mmm donuts!"           -- a := Char
11

>>> len [[1], [1,2], [1,2,3]]   -- a := ???
3
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## Built-in Lists?

This is exactly how Haskell's "built-in" lists are defined:

```haskell
data [a]    = [] | (:) a [a]

data List a = Nil | Cons a (List a)
```

- `Nil` is called `[]` 
- `Cons` is called `:`

Many list manipulating functions e.g. in [Data.List][1] are *polymorphic*
- Can be reused across all kinds of lists.

```haskell
(++) :: [a] -> [a] -> [a]
head :: [a] -> a
tail :: [a] -> [a]
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Generalizing Other Data Types

Polymorphic trees

```haskell
data Tree a 
   = Leaf a 
   | Node (Tree a) (Tree a) 
   deriving (Show)
```

Polymorphic *2-3* trees

```haskell
data Tree23 a 
   = Leaf0  
   | Node2 (Tree23 a) (Tree23 a)
   | Node3 (Tree23 a) (Tree23 a) (Tree23 a)
   deriving (Show)
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Kinds

`List a` corresponds to *lists of values* of type `a`. 

If `a` is the *type parameter*, then what is `List`? 

A *type-constructor* that 
- takes *as input* a type `a`
- returns *as output* the type `List a` 

But wait, if `List` is a *type-constructor* then what is its "type"? 

- A *kind* is the "type" of a type.

```haskell
>>> :kind Int
Int :: *
>>> :kind Char
Char :: *
>>> :kind Bool
Bool :: *
```

Thus, `List` is a function from any "type" to any other "type", and so 

```haskell
>>> :kind List
List :: * -> *
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


## QUIZ 

What is the *kind* of `->`? That, is what does GHCi say if we type

```haskell
>>> :kind (->) 
```

**A.** `*`

**B.** `* -> *`

**C.** `* -> * -> *`

We will not dwell too much on this now. 

As you might imagine, they allow for all sorts of abstractions over data. 

If interested, see [this for more information about kinds](http://en.wikipedia.org/wiki/Kind_(type_theory)). 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
