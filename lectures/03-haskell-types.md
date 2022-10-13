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

5. *Polymorphic Datatypes:* datatypes with parameters

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
circ0 = (0, 0, 100)  -- circle at "origin" with radius 100

cub0 :: CuboidT
cub0 = (10, 20, 30)  -- cuboid with l=10, d=20, h=30 
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
circ0 = (0, 0, 100)  -- circle at "origin" with radius 100

cub0 :: CuboidT
cub0 = (10, 20, 30)  -- cuboid with length=10, depth=20, height=30 

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

(I) final    

    *Answer:* A

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

5. *Polymorphic Datatypes:* datatypes with parameters

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

We can avoid mixing up values by creating _new_ `data` types

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
circ1 :: Circle 
circ1 = MkCircle 0 0 100  -- circle at "origin" w/ radius 100

cub1 :: Cuboid
cub1 = MkCuboid 10 20 30  -- cuboid w/ len=10, dep=20, ht=30 
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
-- | A new type `Circle` with constructor `MkCircle`
data Circle = MkCircle Double Double Double
```

What is the **type of** the `MkCircle` _constructor_?

**A.** `MkCircle :: Circle`

**B.** `MkCircle :: Double -> Circle`

**C.** `MkCircle :: Double -> Double -> Circle`

**D.** `MkCircle :: Double -> Double -> Double -> Circle`

**E.** `MkCircle :: (Double, Double, Double) -> Circle`

(I) final    

    *Answer:* D

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

(I) final    

    *Answer:* B

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

5. *Polymorphic Datatypes:* datatypes with parameters

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
circ1 = MkCircle 0 0 100  -- circle at "origin" with radius 100

cub1 :: Cuboid
cub1 = MkCuboid 10 20 30  -- cuboid with length=10, depth=20, height=30 
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
  = MkCircle Double Double Double   -- Circle at x, y with radius r 
  | MkCuboid Double Double Double   -- Cuboid with length, depth, height
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
  = MkCircle Double Double Double   -- Circle at x, y with radius r 
  | MkCuboid Double Double Double   -- Cuboid with length, depth, height
```

What is the type of `MkCircle 0 0 100` ? 

**A.** `Shape`

**B.** `Circle`

**C.** `MkCircle`

**D.** `(Double, Double, Double)`

(I) final    

    *Answer:* A

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
circ2 = MkCircle 0 0 100  -- circle at "origin" with radius 100

cub2 :: Shape 
cub2 = MkCuboid 10 20 30  -- cuboid with length=10, depth=20, height=30 
```

and then define collections of `Shape`s

```haskell
shapes :: [Shape]
shapes = [circ2, cub2]
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
  = MkRect Double Double -- rectangle with width and height
  | MkCirc Double        -- circle with radius
  | MkPoly [Vertex]      -- polygon with a list of vertices

type Vertex = (Double, Double)
```

Different constructors can have different types!

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

A values of type `Shape2D` is either two doubles *tagged* with `Rectangle` 

```haskell
>>> :type (Rectangle 4.5 1.2)
(Rectangle 4.5 1.2) :: Shape
```

or a single double *tagged* with `Circle`

```haskell
>>> :type (Circle 3.2)
(Circle 3.2) :: Shape
```

or a list of pairs of d *tagged* with `Polygon`

```haskell
ghci> :type (Polygon [(1, 1), (2, 2), (3, 3)])
(Polygon [(1, 1), (2, 2), (3, 3)]) :: Shape
```

<br>
<br>
<br>

![Data values are **Tagged Boxes**](/static/img/lec4_boxed.png)


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
data Shape2D = MkRect Double Double | MkCirc Double | MkPoly [Vertex]
type Vertex = (Double, Double)

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

5. *Polymorphic Datatypes:* datatypes with parameters

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
  = INil                -- empty list
  | ICons Int IntList   -- list with "hd" Int and "tl" IntList
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

## QUIZ 

```haskell
data IntList 
  = INil                -- empty list
  | ICons Int IntList   -- list with "hd" Int and "tl" IntList
```

What is the type of `ICons` ?

**A.** `IntList`

**B.** `Int -> IntList`

**C.** `(Int, IntList)`

**D.** `Int -> IntList -> IntList`

**E.** `IntList -> IntList`

(I) final    

    *Answer:* D


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

Write down an `IntList` representation of the list `[1,2,3]`

```haskell
list_1_2_3 :: IntList
list_1_2_3 = ???
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

Recursion means boxes *within* boxes

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


## Recursive functions over recursive data

Lets rewrite the `count0` function from last lecture to work on `IntList`s:

```haskell
count0 :: IntList -> Int
count0 xs = ???
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

```haskell
count0 :: IntList -> Int
count0 INil         = 0
count0 (ICons 0 xs) = 1 + count0 xs
count0 (ICons _ xs) = count0 xs
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

## Trees

Lists are *unary trees*:

![Unary tree (aka list)](/static/img/list-tree.png){#fig:boxes .align-center width=50%}  

<br>
<br>
<br>

How do we represent *binary trees*?

![Binary tree](/static/img/tree-data-node.png){#fig:boxes .align-center width=80%}  

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## QUIZ: Binary trees

How do you represent this *binary tree* as a recursive datatype?

![Binary tree](/static/img/tree-data-node.png){#fig:boxes .align-center width=50%}
  
**(A)** `data ITree = ILeaf | INode Int ITree`

**(B)** `data ITree = ILeaf | INode ITree ITree`

**(C)** `data ITree = ILeaf | INode Int ITree ITree`

**(D)** `data ITree = ILeaf Int | INode ITree ITree`

**(E)** `data ITree = ILeaf Int | INode Int ITree ITree`

<br>

(I) final

    *Answer:* C
    

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>  

![Binary tree](/static/img/tree-data-node.png){#fig:boxes .align-center width=50%}

```haskell
-- | Binary tree of integers
data ITree = ILeaf | INode Int ITree ITree

t1234 = INode 1 
          (INode 2 (INode 3 ILeaf ILeaf) ILeaf) 
          (INode 4 ILeaf ILeaf)
```

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

3. *Sum Types:* types with multiple variants  \[done\]

4. *Recursive Types:* types that contain themselves  \[done\]

5. ***Polymorphic Datatypes:* datatypes with parameters**

<br>
<br>
<br>
<br>
<br>
<br>
<br>


## Parameterized Types

Our `IntList` datatype can only store `Int`s :-(

What if we want to store `Char`s or `Double`s?

```haskell
data CharList 
  = CNil
  | CCons Char CharList

data DoubleList 
   = DNil
   | DCons Char DoubleList
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

<br>
<br>
<br>
<br>

**Common:** `Nil`/`Cons` structure

**Different:** type of each "head" element

<br>
<br>
<br>
<br>

### Refactored using Type Parameter

```haskell
-- | A list of elements of type `a`
data List a = Nil | Cons a  (List a)
```

We can recover original types as *instances* of `List`:

```haskell
iList :: List Int      -- list where 'a' = 'Int' 
iList = Cons 1 (Cons 2 (Cons 3 Nil))

cList :: List Char     -- list where 'a' = 'Char' 
cList = Cons 'a' (Cons 'b' (Cons 'c' Nil))

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

## QUIZ 

```haskell
data List a = Nil | Cons a  (List a)
```

What is the type of `Cons` ?

**A.** `Int ->  List      -> List`

**B.** `Int ->  List Int  -> List Int`

**C.** `Char -> List Char -> List Char`

**D.** `a    -> List      -> List`

**E.** `a    -> List a    -> List a`

(I) final    

    *Answer:* E


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

## EXERCISE: Polymorphic Functions

Write an `append` function that appends two `List`s:

```haskell
data List a = Nil | Cons a  (List a)

append :: ??? -- What is the type of `append`?
append = ???
```

so that we can call:

```haskell
-- Using built-in list syntax for readability:
>>> append [1.1, 2.2] [3.3, 4.4]
[1.1, 2.2, 3.3, 4.4]

>>> append "mmm, " "donuts!"
"mmm, donuts!"
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

## Polymorphic Functions over Polymorphic Data

The `append` function on `List`s is polymorphic:

```haskell
append :: List a -> List a -> List a
append Nil ys         = ys
append (Cons x xs) ys = Cons x (append xs ys)
``` 

`append` doesn't care about the actual *values* in the list

- only manipulates the *structure* of the list



Hence `append :: List a -> List a -> List a` 

- we can call `append` on lists **of any kind**
- as long as both lists are of **the same kind**

```haskell
>>> append [1.1, 2.2] [3.3, 4.4]  -- a = Double
[1.1, 2.2, 3.3, 4.4]

>>> append "mmm, " "donuts!"      -- a = Char
"mmm, donuts!"

>>> append [1, 2] "donuts!"       -- a = ???
???

>>> append [[1], [1,2]] [[1,2,3]] -- a := ???
???
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

Many list manipulating functions e.g. in `Data.List` are *polymorphic*
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

(I) final    

    *Answer:* C

<br>
<br>
<br>
<br>
<br>

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
