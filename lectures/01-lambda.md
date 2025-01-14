---
title: Lambda Calculus
headerImg: sea.jpg
---

## Your Favorite Language

Probably has lots of features:

* Assignment (`x = x + 1`)
* Booleans, integers, characters, strings, ...
* Conditionals
* Loops
* `return`, `break`, `continue`
* Functions
* Recursion
* References / pointers
* Objects and classes
* Inheritance
* ...

Which ones can we do without?

What is the **smallest universal language**?

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
<br>
<br>
<br>

## What is computable?

### Before 1930s

Informal notion of an **effectively calculable** function:

![can be computed by a human with pen and paper, following an algorithm](https://oercommons.s3.amazonaws.com/media/courseware/assets/G06/06-math-math-06-9780328761197-math-9780328761197-ah-studio-images-ip3-mth-6-2-8-2-1_mw-4x3_dividehandwritten-ip3.png){#fig:pen-and-paper .align-center width=40%}


<br>
<br>
<br>
<br>

### 1936: Formalization

What is the **smallest universal language**?

![Alan Turing](https://upload.wikimedia.org/wikipedia/commons/a/a1/Alan_Turing_Aged_16.jpg){#fig:turing .align-center width=40%}

(I) final

    The [**Turing Machine**](https://en.wikipedia.org/wiki/Turing_machine)
    
<br>
<br>    
 
![Alonzo Church](https://upload.wikimedia.org/wikipedia/en/a/a6/Alonzo_Church.jpg){#fig:church .align-center width=40%}

(I) final

    The **Lambda Calculus**

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

## The Next 700 Languages

![Peter Landin](https://upload.wikimedia.org/wikipedia/en/f/f9/Peter_Landin.png){#fig:landin .align-center width=40%}

> Whatever the next 700 languages
> turn out to be,
> they will surely be
> variants of lambda calculus.

Peter Landin, 1966


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

## The Lambda Calculus

Has one feature:

* Functions

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

No, *really*

* ~~Assignment (`x = x + 1`)~~
* ~~Booleans, integers, characters, strings, ...~~
* ~~Conditionals~~
* ~~Loops~~
* ~~`return`, `break`, `continue`~~
* Functions
* ~~Recursion~~
* ~~References / pointers~~
* ~~Objects and classes~~
* ~~Inheritance~~
* ~~Reflection~~

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

More precisely, *only thing* you can do is:

* **Define** a function
* **Call** a function

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

## Describing a Programming Language

* _Syntax:_ what do programs look like?
* _Semantics:_ what do programs mean?
    * _Operational semantics_: how do programs execute step-by-step?

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

## Syntax: What Programs _Look Like_

<br>

```haskell
e ::= x
    | \x -> e
    | e1 e2
```

<br>

Programs are **expressions** `e` (also called **$\lambda$-terms**)
of one of three kinds:

- **Variable**
    - `x`, `y`, `z`
- **Abstraction** (aka _nameless_ function definition)
    - `\x -> e`
    - `x` is the _formal_ parameter, `e` is the _body_ 
    - "for any `x` compute `e`"
- **Application** (aka function call)
    - `e1 e2`
    - `e1` is the _function_, `e2` is the _argument_
    - in your favorite language: `e1(e2)`

(Here each of `e`, `e1`, `e2` can itself be a variable, abstraction, or application)

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

## Examples

```haskell
\x -> x             -- The identity function (id)
                    -- ("for any x compute x")

\x -> (\y -> y)     -- A function that returns (id)

\f -> (f (\x -> x)) -- A function that applies its argument to id 
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


## QUIZ

Which of the following terms are syntactically **incorrect**?

**A.**  `\(\x -> x) -> y`

**B.**  `\x -> x x`

**C.**  `\x -> x (y x)`

**D.**  A and C

**E.**  all of the above

<br>

(I) final

    _Correct answer:_ **A**



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

## Examples

```haskell
\x -> x             -- The identity function
                    -- ("for any x compute x")

\x -> (\y -> y)     -- A function that returns the identity function
 
\f -> f (\x -> x)   -- A function that applies its argument 
                    -- to the identity function
```

<br>

How do I define a function with two arguments?

* e.g. a function that takes `x` and `y` and returns `y`?

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

```haskell
\x -> (\y -> y)     -- A function that returns the identity function
                    -- OR: a function that takes two arguments
                    -- and returns the second one!
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

How do I apply a function to two arguments?

* e.g. apply `\x -> (\y -> y)` to `apple` and `banana`?

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

```haskell
(((\x -> (\y -> y)) apple) banana) -- first apply to apple,
                                   -- then apply the result to banana
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




## Syntactic Sugar

<br>
<br>

instead of                |  we write
:-------------------------|:-------------------------
`\x -> (\y -> (\z -> e))` | `\x -> \y -> \z -> e`
`\x -> \y -> \z -> e`     | `\x y z -> e`
`(((e1 e2) e3) e4)`       |  `e1 e2 e3 e4`

<br>
<br>

```haskell
\x y -> y     -- A function that that takes two arguments
              -- and returns the second one...
              
(\x y -> y) apple banana -- ... applied to two arguments
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

## Semantics : What Programs _Mean_

<br>

How do I "run" / "execute" a $\lambda$-term?

<br>

Think of middle-school algebra:

```haskell
-- Simplify expression:
  (x + 2)*(3x - 1)
=> -- RULE: multiply polynomials
  3x^2 - x + 6x - 2
=> -- RULE: add monomials
  3x^2 + 5x - 2
```

<br>

**Execute** = rewrite step-by-step 

- Following simple *rules*
- until no more rules *apply*

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

## Rewrite Rules of Lambda Calculus

<br>

1. $\beta$-step   (aka _function call_)
2. $\alpha$-step  (aka _renaming formals_)

<br>

But first we have to talk about **scope**

<br>
<br>
<br>
<br>
<br>
<br>

## Semantics: Scope of a Variable

The part of a program where a **variable is visible**

In the expression `\x -> e`

- `x` is the newly introduced variable

- `e` is **the scope** of `x`

- any occurrence of `x` in `\x -> e` is **bound** (by the **binder** `\x`)

<br>

For example, `x` is bound in:

```
  \x -> x
  \x -> (\y -> x)
```

<br>
<br>

An occurrence of `x` in `e` is **free** if it's _not bound_ by an enclosing abstraction

<br>
For example, `x` is free in:

```
  x y                -- no binders at all!  
  \y -> x y          -- no \x binder
  (\x -> \y -> y) x  -- x is outside the scope of the \x binder;
                     -- intuition: it's not "the same" x
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

## QUIZ

In the expression `(\x -> x) x`,
is `x` _bound_ or _free_?

**A.**  first occurrence is bound, second is bound 

**B.**  first occurrence is bound, second is free

**C.**  first occurrence is free, second is bound

**D.**  first occurrence is free, second is free 

<br>

(I) final
    
    _Correct answer:_ **B**

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


## EXERCISE: Free Variables

A variable `x` is **free** in `e` if *there exists* a free occurrence of `x` in `e`

<br>


We can formally define the set of _all free variables_ in a term like so:

(I) lecture

    ```haskell
    FV(x)       = ???
    FV(\x -> e) = ???
    FV(e1 e2)   = ???
    ```

(I) final

    ```haskell
    FV(x)       = {x}
    FV(\x -> e) = FV(e)  - {x}
    FV(e1 e2)   = FV(e1) + FV(e2)
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


## Closed Expressions

If `e` has _no free variables_ it is said to be **closed**

- Closed expressions are also called **combinators**

<br>
<br>

What is the shortest closed expression?

(I) final

    _Answer:_ `\x -> x`

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

## Rewrite Rules of Lambda Calculus

<br>

1. $\beta$-step   (aka _function call_)
2. $\alpha$-step  (aka _renaming formals_)

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

## Semantics: Redex

A **redex** (*red*ucible *ex*pression) is a term of the form

<br>

```
  (\x -> e1) e2
```

A *function* `(\x -> e1)` 


- `x` is the *parameter*
- `e1` is the *returned* expression

*Applied to* an argument `e2`

- `e2` is the *argument* 

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

## Semantics: $\beta$-Reduction

<br>

A **redex** b-steps to another term ...

```
  (\x -> e1) e2   =b>   e1[x := e2]
```

<br>

where `e1[x := e2]` means

"`e1` with all _free_ occurrences of `x` replaced with `e2`"

<br>
<br>

Computation by _search-and-replace_:

- If you see an _abstraction_ applied to an _argument_,
take the _body_ of the abstraction and
replace all free occurrences of the _formal_ by that _argument_

- We say that `(\x -> e1) e2` $\beta$-steps to `e1[x := e2]`



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

## Redex Examples

<br>

```haskell
(\x -> x) apple     
=b> apple
```

Is this right? Ask [Elsa](http://goto.ucsd.edu/elsa/index.html)! (https://goto.ucsd.edu/elsa/index.html)

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

<br>

```haskell
(\x -> y x y x) apple
=b> ???
```

**A.** `apple apple apple apple`

**B.** `y apple y apple`

**C.** `y y y y`

**D.** `apple` 

<br>

(I) final

    _Correct answer:_ **B.**

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

<br>

```haskell
(\x -> (\y -> y)) apple
=b> ???
```

**A.** `apple`

**B.** `\y -> apple`

**C.** `\x -> apple`

**D.** `\y -> y`

**E.** `\x -> y`


<br>

(I) final

    _Correct answer:_ **D.**

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

<br>

```haskell
(\x -> x (\x -> x)) apple
=b> ???
```

**A.** `apple (\x -> x)`

**B.** `apple (\apple -> apple)`

**C.** `apple (\x -> apple)`

**D.** `apple`

**E.** `\x -> x`


<br>

(I) final

    _Correct answer:_ **A.**
    
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

What is a $\lambda$-term `fill_this_in` such that

<br>

```haskell
fill_this_in apple
=b> banana
```

ELSA: https://goto.ucsd.edu/elsa/index.html

[Click here to try this exercise](https://goto.ucsd.edu/elsa/index.html#?demo=permalink%2F1585434473_24432.lc)

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

## A Tricky One

<br>

```haskell
(\x -> (\y -> x)) y
=b> \y -> y
```

Is this right?

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

## Something is Fishy

<br>

```haskell
(\x -> (\y -> x)) y
=b> \y -> y
```

Is this right?

**Problem**: The *free* `y` in the argument has been **captured** by `\y` in *body*!

<br>

**Solution**: Ensure that *formals* in the body are **different from** *free-variables* of argument! 

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

## Capture-Avoiding Substitution

We have to fix our definition of $\beta$-reduction:

```
  (\x -> e1) e2   =b>   e1[x := e2]
```
<br>
where `e1[x := e2]` means ~~"`e1` with all _free_ occurrences of `x` replaced with `e2`"~~

  - `e1` with all _free_ occurrences of `x` replaced with `e2`
  - **as long as** no free variables of `e2` get captured

<br>  

Formally:

```haskell
x[x := e]            = e

y[x := e]            = y          -- when x /= y

(e1 e2)[x := e]      = (e1[x := e]) (e2[x := e])

(\x -> e1)[x := e]   = \x -> e1   -- Q: Why leave `e1` unchanged?

(\y -> e1)[x := e] 
  | not (y in FV(e)) = \y -> e1[x := e]
```

**Oops, but what to do if** `y` is in the *free-variables* of `e`? 

  - i.e. if `\y -> ...` may *capture* those free variables?

(I) final
    
    *Answer*: We leave `e1` above alone even though it might contain `x`, 
    because in `\x -> e1` every occurrence of `x` is bound by `\x`
    (hence, there are *no free occurrences* of `x`)

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



## Rewrite Rules of Lambda Calculus

<br>

1. $\beta$-step   (aka _function call_)
2. $\alpha$-step  (aka _renaming formals_)

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

## Semantics: $\alpha$-Renaming

<br>

```haskell
  \x -> e   =a>   \y -> e[x := y]
    where not (y in FV(e))
```
<br>

- We rename a formal parameter `x` to `y` 

- By replace all occurrences of `x` in the body with `y`

- We say that `\x -> e` $\alpha$-steps to `\y -> e[x := y]`

<br>
<br>

Example:

```haskell
\x -> x   =a>   \y -> y   =a>    \z -> z
```

All these expressions are **$\alpha$-equivalent**

<br>
<br>
<br>

What's wrong with these?

```haskell
-- (A)
\f -> f x    =a>   \x -> x x
```

(I) final

    *Answer:* it violates the side-condition for $\alpha$-renaming 
    that the new formal (`x`) must not occur freely in the body 

```haskell
-- (B)
(\x -> \y -> y) y   =a>   (\x -> \z -> z) z
```

(I) final
     
    *Answer:* we should only rename within the body of the abstraction; 
    the second `y` is a free variable, and hence must remain unchanged     

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


## Tricky Example Revisited

<br>

```haskell
    (\x -> (\y -> x)) y
                                -- rename 'y' to 'z' to avoid capture
    =a> (\x -> (\z -> x)) y
                                -- now do b-step without capture!
    =b> \z -> y
```
    
<br>
<br>
To avoid getting confused, 

- you can **always rename** formals, 

- so different **variables** have different **names**!

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



## Normal Forms

Recall **redex** is a $\lambda$-term of the form

`(\x -> e1) e2`

A $\lambda$-term is in **normal form** if it *contains no redexes*.

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

Which of the following term are **not** in _normal form_ ?

**A.** `x y`

**B.** `(\x -> x) y`

**C.** `x (\y -> y)`

**D.** `z ((\x -> x) y)`

**E.** B and D

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
<br>
<br>
<br>



## Semantics: Evaluation

A $\lambda$-term `e` **evaluates to** `e'` if

1. There is a sequence of steps

    ```haskell
    e =?> e_1 =?> ... =?> e_N =?> e'
    ```

   where each `=?>` is either `=a>` or `=b>` 
   and `N >= 0`

2. `e'` is in _normal form_


<br>
<br>
<br>
<br>
<br>
<br>


## Examples of Evaluation

```haskell
(\x -> x) apple
  =b> apple
```

<br> 

(I) lecture
         
    ```haskell
    (\f -> (\x -> x) f) (\x -> x)
      =?> ???
    ```
    
(I) final
         
    ```haskell
    (\f -> f (\x -> x)) (\x -> x)
      =b> (\x -> x) (\x -> x)
      =b> \x -> x
    ```
    
<br>    

(I) lecture
    
    ```haskell
    (\x -> x x) (\x -> x)
      =?> ???
    ```

(I) final
         
    ```haskell
    (\x -> x x) (\x -> x)
      =b> (\x -> x) (\x -> x)
      =b> \x -> x
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

## EXERCISE

What is a $\lambda$-term `fill_this_in` such that the evaluation of
`(\x -> x x) fill_this_in` *loops*, i.e.:

```haskell
eval loop : 
  (\x -> x x) fill_this_in
  =b> (\x -> x x) fill_this_in
  =b> (\x -> x x) fill_this_in
  =b> ...
```

ELSA: https://goto.ucsd.edu/elsa/index.html

[Click here to try this exercise](https://goto.ucsd.edu/elsa/index.html#?demo=permalink%2F1664296539_173491.lc)

<br>
<br>
<br>
<br>
<br>
<br>
<br>

## Non-Terminating Evaluation

```haskell
(\x -> x x) (\x -> x x)
  =b> (\x -> x x) (\x -> x x)
```

Some programs loop back to themselves...

... and *never* reduce to a normal form!

This combinator is called $\Omega$

<br>
<br>
<br>
<br>
<br>
<br>


## Elsa shortcuts

Named $\lambda$-terms:

```
let ID = \x -> x  -- abbreviation for \x -> x
```

<br>
<br>

To substitute name with its definition, use a `=d>` step:

```haskell
ID apple
  =d> (\x -> x) apple    -- expand definition
  =b> apple              -- beta-reduce
```

<br>
<br>

Evaluation:

- `e1 =*> e2`: `e1` reduces to `e2` in 0 or more steps
    - where each step is `=a>`, `=b>`, or `=d>`
- `e1 =~> e2`: `e1` evaluates to `e2` and `e2` is **in normal form**


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

## Programming in $\lambda$-calculus

*Real languages have lots of features*

- Functions \[we got those\]
- Booleans
- Records (structs, tuples)
- Numbers
- Lists
- Recursion

Lets see how to _encode_ all of these features
with the $\lambda$-calculus.


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

## $\lambda$-calculus: Booleans

<br>

How can we encode Boolean values (`TRUE` and `FALSE`) as functions?

<br>

Well, what do we **do** with a Boolean `b`?

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


Make a *binary choice*

  - `if b then e1 else e2`

<br>
<br>
<br>

## Booleans: API

We need to define three functions

```haskell
let TRUE  = ???
let FALSE = ???
let ITE   = \b x y -> ???  -- if b then x else y
```

such that

```haskell
ITE TRUE apple banana =~> apple
ITE FALSE apple banana =~> banana
```

(Here, `let NAME = e` means `NAME` is an _abbreviation_ for `e`)


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

## Booleans: Implementation

```haskell
let TRUE  = \x y -> x        -- Returns its first argument
let FALSE = \x y -> y        -- Returns its second argument
let ITE   = \b x y -> b x y  -- Applies condition to branches
                             -- (redundant, but improves readability)
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



## Example: Branches step-by-step


```haskell
eval ite_true:
  ITE TRUE e1 e2
  =d> (\b x y -> b    x  y) TRUE e1 e2    -- expand def ITE  
  =b>   (\x y -> TRUE x  y)      e1 e2    -- beta-step
  =b>     (\y -> TRUE e1 y)         e2    -- beta-step
  =b>            TRUE e1 e2               -- expand def TRUE
  =d>     (\x y -> x) e1 e2               -- beta-step
  =b>       (\y -> e1)   e2               -- beta-step
  =b> e1
```


<br>
<br>
<br>
<br>
<br>
<br>

## Example: Branches step-by-step

Now you try it!

Can you [fill in the blanks to make it happen?][elsa-ite]


(I) lecture

    ```haskell
    eval ite_false:
      ITE FALSE e1 e2

      -- fill the steps in!

      =b> e2  
    ```

(I) final

    ```haskell
    eval ite_false:
      ITE FALSE e1 e2
      =d> (\b x y -> b     x  y) FALSE e1 e2   -- expand def ITE  
      =b>   (\x y -> FALSE x  y)       e1 e2   -- beta-step
      =b>     (\y -> FALSE e1 y)          e2   -- beta-step
      =b>            FALSE e1 e2               -- expand def FALSE
      =d>      (\x y -> y) e1 e2               -- beta-step
      =b>        (\y -> y)    e2               -- beta-step
      =b> e2
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




## EXERCISE: Boolean Operators

ELSA: https://goto.ucsd.edu/elsa/index.html

[Click here to try this exercise](https://goto.ucsd.edu/elsa/index.html#?demo=permalink%2F1585435168_24442.lc)

Now that we have `ITE` it's easy to define other Boolean operators:

(I) lecture

    ```haskell
    let NOT = \b     -> ???
    let OR  = \b1 b2 -> ???
    let AND = \b1 b2 -> ???
    ```

(I) final 

    ```haskell
    let NOT = \b     -> ITE b FALSE TRUE 
    
    let AND = \b1 b2 -> ITE b1 b2 FALSE
    
    let OR  = \b1 b2 -> ITE b1 TRUE b2
    ```

When you are done, you should get the following behavior:

```haskell
eval ex_not_t:
  NOT TRUE =*> FALSE
  
eval ex_not_f:
  NOT FALSE =*> TRUE 
  
eval ex_or_ff:
  OR FALSE FALSE =*> FALSE

eval ex_or_ft:
  OR FALSE TRUE =*> TRUE
  
eval ex_or_ft:
  OR TRUE FALSE =*> TRUE

eval ex_or_tt:
  OR TRUE TRUE =*> TRUE
  
eval ex_and_ff:
  AND FALSE FALSE =*> FALSE

eval ex_and_ft:
  AND FALSE TRUE =*> FALSE
  
eval ex_and_ft:
  AND TRUE FALSE =*> FALSE

eval ex_and_tt:
  AND TRUE TRUE =*> TRUE
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

## Programming in $\lambda$-calculus

- Functions \[we got those\]
- Booleans \[done\]
- Records (structs, tuples)
- Numbers
- Lists
- Recursion

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

## $\lambda$-calculus: Records

Let's start with records with _two_ fields (aka **pairs**)

What do we *do* with a pair?

1. **Pack two** items into a pair, then
2. **Get first** item, or
3. **Get second** item.


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

## Pairs : API

We need to define three functions

```haskell
let PAIR = \x y -> ???    -- Make a pair with elements x and y 
                          -- { fst : x, snd : y }
let FST  = \p -> ???      -- Return first element 
                          -- p.fst
let SND  = \p -> ???      -- Return second element
                          -- p.snd
```

such that

```haskell
eval ex_fst: 
  FST (PAIR apple banana) =*> apple

eval ex_snd:
  SND (PAIR apple banana) =*> banana
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


## Pairs: Implementation

A pair of `x` and `y` is just something that lets you pick between `x` and `y`!
(i.e. a function that takes a boolean and returns either `x` or `y`)  

```haskell
let PAIR = \x y -> (\b -> ITE b x y)
let FST  = \p -> p TRUE   -- call w/ TRUE, get first value
let SND  = \p -> p FALSE  -- call w/ FALSE, get second value
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


## EXERCISE: Triples

How can we implement a record that contains **three** values?

ELSA: https://goto.ucsd.edu/elsa/index.html

[Click here to try this exercise](https://goto.ucsd.edu/elsa/index.html#?demo=permalink%2F1585434814_24436.lc)

(I) lecture

```haskell
let TRIPLE = \x y z -> ???
let FST3   = \t -> ???
let SND3   = \t -> ???
let THD3   = \t -> ???

eval ex1:
  FST3 (TRIPLE apple banana orange)
  =*> apple

eval ex2:
  SND3 (TRIPLE apple banana orange)
  =*> banana 

eval ex3:
  THD3 (TRIPLE apple banana orange)
  =*> orange
```

(I) final

    ```haskell
    let TRIPLE = \x y z -> PAIR x (PAIR y z)
    let FST3  = \t -> FST t
    let SND3  = \t -> FST (SND t)
    let THD3  = \t -> SND (SND t)
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

## Programming in $\lambda$-calculus

- Functions \[we got those\]
- Booleans \[done\]
- Records (structs, tuples) \[done\]
- Numbers
- Lists
- Recursion

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

## $\lambda$-calculus: Numbers

Let's start with **natural numbers** (0, 1, 2, ...)

What do we *do* with natural numbers?

- Count: `0`, `inc`
- Arithmetic: `dec`, `+`, `-`, `*`
- Comparisons: `==`, `<=`, etc

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

## Natural Numbers: API

We need to define:

- A family of **numerals**: `ZERO`, `ONE`, `TWO`, `THREE`, ...
- Arithmetic functions: `INC`, `DEC`, `ADD`, `SUB`, `MULT`
- Comparisons: `IS_ZERO`, `EQ`

Such that they respect all regular laws of arithmetic, e.g.

```haskell
IS_ZERO ZERO       =~> TRUE
IS_ZERO (INC ZERO) =~> FALSE
INC ONE            =~> TWO
...
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

## Natural Numbers: Implementation

**Church numerals**: _a number `N`_
is encoded as a combinator that
_calls a function on an argument `N` times_

```haskell
let ONE   = \f x -> f x
let TWO   = \f x -> f (f x)
let THREE = \f x -> f (f (f x))
let FOUR  = \f x -> f (f (f (f x)))
let FIVE  = \f x -> f (f (f (f (f x))))
let SIX   = \f x -> f (f (f (f (f (f x)))))
...
```


## QUIZ: Church Numerals

Which of these is a valid encoding of `ZERO` ?

- **A**: `let ZERO = \f x -> x`

- **B**: `let ZERO = \f x -> f`

- **C**: `let ZERO = \f x -> f x`

- **D**: `let ZERO = \x -> x`

- **E**: None of the above

(I) final

    *Answer:* A

<br>
<br>
<br>

Does this function look familiar?

(I) final

    *Answer:* It's the same as `FALSE`!

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


## $\lambda$-calculus: Increment

(I) lecture

    ```haskell
    -- Call `f` on `x` one more time than `n` does
    let INC   = \n -> (\f x -> ???)
    ```
    
(I) final

    ```haskell
    -- Call `f` on `x` one more time than `n` does
    let INC   = \n -> (\f x -> f (n f x))
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

**Example:**

```haskell
eval inc_zero :
  INC ZERO
  =d> (\n f x -> f (n f x)) ZERO
  =b> \f x -> f (ZERO f x)
  =*> \f x -> f x
  =d> ONE
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

## EXERCISE 

Fill in the implementation of `ADD` so that you get the following behavior


[Click here to try this exercise](https://goto.ucsd.edu/elsa/index.html#?demo=permalink%2F1585436042_24449.lc)

```haskell
let ZERO = \f x -> x
let ONE  = \f x -> f x
let TWO  = \f x -> f (f x)
let INC  = \n f x -> f (n f x)

let ADD  = fill_this_in 

eval add_zero_zero: 
  ADD ZERO ZERO =~> ZERO

eval add_zero_one: 
  ADD ZERO ONE =~> ONE

eval add_zero_two: 
  ADD ZERO TWO =~> TWO 

eval add_one_zero: 
  ADD ONE ZERO =~> ONE

eval add_one_zero: 
  ADD ONE ONE =~> TWO

eval add_two_zero: 
  ADD TWO ZERO =~> TWO  
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

$\lambda$-calculus: Addition


```haskell
--  Call `f` on `x` exactly `n + m` times
let ADD = \n m -> n INC m
```

<br>
<br>
<br>

**Example:**

```haskell
eval add_one_zero :
  ADD ONE ZERO
  =~> ONE
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


## QUIZ

How shall we implement `MULT`?

**A.**  `let MULT = \n m -> n ADD m`

**B.**  `let MULT = \n m -> n (ADD m) ZERO`

**C.**  `let MULT = \n m -> m (ADD n) ZERO`

**D.**  `let MULT = \n m -> n (ADD m ZERO)`

**E.**  `let MULT = \n m -> (n ADD m) ZERO`

(I) final

    *Answer:* B or C

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

## $\lambda$-calculus: Multiplication

```haskell
--  Call `f` on `x` exactly `n * m` times
let MULT = \n m -> n (ADD m) ZERO
```

<br>
<br>
<br>

**Example:**

```haskell
eval two_times_three :
  MULT TWO ONE
  =~> TWO
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

## Programming in $\lambda$-calculus

- Functions \[we got those\]
- Booleans \[done\]
- Records (structs, tuples) \[done\]
- Numbers \[done\]
- Lists
- Recursion

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

## $\lambda$-calculus: Lists

Records had *fixed* length:

```haskell
PAIR apple banana
TRIPLE apple banana cherry
```

Now we want to build lists of *arbitrary* length.

Can we do it like this?

```haskell
LIST apple banana
LIST apple banana cherry
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

That's unlikely to work (requires a function with a variable number of arguments).

But we can construct lists like this:
  
```haskell
CONS apple (CONS banana NIL)
CONS apple (CONS banana (CONS cherry NIL))
```

where

- `NIL` denotes the empty list
- `CONS h t` denotes a non-empty list with head `h` and tail `t`

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

**Destructing a list**

- `HEAD l` returns the _first_ element of the list
- `TAIL l` returns the _rest_ of the list

```haskell
HEAD (CONS apple (CONS banana (CONS cherry NIL)))
=*> apple

TAIL (CONS apple (CONS banana (CONS cherry NIL)))
=*> CONS banana (CONS cherry NIL)
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

## Lists: API

We need to define five functions

```haskell
let CONS = ???
let HEAD = ???
let TAIL = ???

let NIL  = ???
let IS_EMPTY = ???
```

such that

```haskell
eval elem0:
  HEAD (CONS apple (CONS banana (CONS cherry NIL)))
  =~> apple

eval elem1: 
  HEAD (TAIL (CONS apple (CONS banana (CONS cherry NIL))))
  =~> banana

eval elem2: 
  HEAD (TAIL (TAIL (CONS apple (CONS banana (CONS cherry NIL)))))
  =~> cherry

eval empty_nil:
  IS_EMPTY NIL
  =~> TRUE

eval empty_cons:
  IS_EMPTY (CONS apple (CONS banana (CONS cherry NIL)))
  =~> FALSE
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

The first three are easy:

```haskell
let CONS = \h t -> PAIR h t
let HEAD = \l -> FST l
let TAIL = \l -> SND l
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

## EXERCISE: Nth

Write an implementation of `GetNth` such that

-  `GetNth n l` returns the n-th element of the list `l` 

*Assume that `l` has n or more elements*

```haskell
let GetNth = ???

eval nth1 :
  GetNth ZERO (CONS apple (CONS banana (CONS cherry NIL)))
  =~> apple 

eval nth1 :
  GetNth ONE (CONS apple (CONS banana (CONS cherry NIL)))
  =~> banana

eval nth2 :
  GetNth TWO (CONS apple (CONS banana (CONS cherry NIL)))
  =~> cherry
```

[Click here to try this in elsa](https://goto.ucsd.edu/elsa/index.html#?demo=permalink%2F1664898475_198478.lc) 

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

## IS_EMPTY and NIL

We need to define `IS_EMPTY` and `NIL` such that

```haskell
IS_EMPTY (CONS e1 e2) =~> FALSE -- for any e1 and e2!

IS_EMPTY NIL =~> TRUE
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>

```haskell
    IS_EMPTY (CONS e1 e2)
=*>  -- by def. of CONS, PAIR
    IS_EMPTY (\b -> b e1 e2)    
=d> -- let's make IS_EMPTY apply its pair to something:
    (\l -> l SOMETHING) (\b -> b e1 e2)
=b>
    (\b -> b e1 e2) SOMETHING
=b>
    SOMETHING e1 e2
=~>
    FALSE
```

What is such a `SOMETHING` that `SOMETHING e1 e2` is always `FALSE`?

<br>
<br>
<br>

```haskell
let SOMETHING = \x y -> FALSE
```

i.e.

```haskell
let IS_EMPTY = \l -> l (\x y -> FALSE)
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

## EXERCISE: NIL

Now define `NIL` such that:

```haskell
let IS_EMPTY = \l -> l (\x y -> FALSE)
let NIL = ???

eval is_empty_nil :
  IS_EMPTY NIL
  =~> TRUE
```

[Click here to try this in elsa](https://goto.ucsd.edu/elsa/index.html#?demo=permalink%2F1664899347_198509.lc)


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

## Programming in $\lambda$-calculus

- Functions \[we got those\]
- Booleans \[done\]
- Records (structs, tuples) \[done\]
- Numbers \[done\]
- Lists \[done\]
- Recursion


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



## $\lambda$-calculus: Recursion

<br>

I want to write a function `LEN` that computes the length of a list, i.e.:

```haskell
eval len_nil: 
  LEN NIL =~> ZERO
  
eval len_1:
  LEN (CONS apple NIL) =~> ONE

eval len_2:
  LEN (CONS apple (CONS banana NIL)) =~> TWO
```

Can we write `LEN` **using Church Numerals**?

<br>
<br>
<br>
<br>
<br>
<br>

Yes, if know the maximum possible length of a list.

[Try it in Elsa!](http://goto.ucsd.edu/elsa/index.html#?demo=permalink%2F1664904972_198787.lc)

But what if we don't?

<br>
<br>
<br>
<br>
<br>
<br>

We need to use recursion!

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

Is this a correct implementation of `LEN`?

```haskell
let LEN = \l -> ITE (IS_EMPTY l) 
                ZERO 
                (INC (LEN (TAIL l)))
```

**A.**  Yes

**B.**  No

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

No! 

  * Named terms in Elsa are just syntactic sugar
  * To translate an Elsa term to $\lambda$-calculus: replace each name with its definition

```haskell
let LEN = \l -> ITE (IS_EMPTY l) 
                ZERO 
                (INC (LEN (TAIL l))) -- But LEN is not a thing!
```

<br>
<br>

**Recursion:** 

 - Inside this function I want to call *the same function* on `TAIL l`

<br>
<br>

Looks like we can't do recursion,
because it requires being able to refer to functions *by name*,
but in $\lambda$-calculus functions are *anonymous*.

Right?

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

## $\lambda$-calculus: Recursion

Think again!

<br>
<br>

**Recursion:** 

 - ~~Inside this function I want to call *the same function* on `TAIL l`~~
 - Inside this function I want to call *a function* on `TAIL l`
 - *And BTW,* I want it to be the same function 
 
<br>
<br>

**Step 1:** Pass in the function to call "recursively"
 
```haskell
let STEP = 
  \rec -> \l -> ITE (IS_EMPTY l) 
                    ZERO 
                    (INC (rec (TAIL l))) -- Call some rec
```
<br>
<br>

**Step 2:** Do something clever to `STEP`, so that the function passed as `rec`
itself becomes

```
\l -> ITE (IS_EMPTY l) ZERO (INC (rec (TAIL l)))
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
 
## $\lambda$-calculus: Fixpoint Combinator 

**Wanted:** a combinator `FIX` such that `FIX STEP`
calls `STEP` with itself as the first argument:

```
FIX STEP
=*> STEP (FIX STEP)
```

<br>

(In math: a *fixpoint* of a function $f(x)$ is a point $x$, such that $f(x) = x$)

<br>
<br>
<br>
<br>

Once we have it, we can define:

```
let LEN = FIX STEP
```

Then by property of `FIX` we have:
```
LEN =*> STEP LEN -- (1)
```


```
LEN (CONS a NIL)
  =*> -- (1) 
STEP LEN (CONS a NIL)
  =d>
(\rec l -> ITE (IS_EMPTY l) ZERO (INC (rec (TAIL l)))) LEN (CONS a NIL)
  =b> 
(\    l -> ITE (IS_EMPTY l) ZERO (INC (LEN (TAIL l))))     (CONS a NIL) 
  =b>                               -- ^^^ the magic happened!
ITE (IS_EMPTY l) ZERO (INC (LEN (TAIL (CONS a NIL))))
=*> -- def of IS_EMPTY, ITE, TAIL, ... 
INC (LEN NIL)
=*> -- (1)
INC (STEP LEN NIL)
=d> 
INC ((\rec l -> ITE (IS_EMPTY l) ZERO (INC (rec (TAIL l)))) LEN NIL)
=b> 
INC ((\l -> ITE (IS_EMPTY l) ZERO (INC (LEN (TAIL l)))) NIL)
=*> 
INC (ITE (IS_EMPTY NIL) ZERO (INC (LEN (TAIL NIL))))
=*> 
INC ZERO
=~> 
ONE
```


How should we define `FIX`???

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

## The Y combinator 
 
Remember $\Omega$?
 
```haskell
(\x -> x x) (\x -> x x)
=b> (\x -> x x) (\x -> x x)
``` 
 
This is *self-replicating code*! We need something like this but a bit more involved...

<br>
<br>
<br>
<br>

The Y combinator discovered by Haskell Curry:

```haskell
let FIX   = \stp -> (\x -> stp (x x)) (\x -> stp (x x))
``` 
<br>
<br>

How does it work?

```haskell
eval fix_step:
  FIX STEP
  =d> (\stp -> (\x -> stp (x x)) (\x -> stp (x x))) STEP
  =b> (\x -> STEP (x x)) (\x -> STEP (x x))
  =b> STEP ((\x -> STEP (x x)) (\x -> STEP (x x)))
  --       ^^^^^^^^^^ this is FIX STEP ^^^^^^^^^^^
``` 

<br>
<br>
<br>
<br>
<br>

That's all folks, Haskell Curry was very clever.

**Next week:** We'll look at the language named after him (`Haskell`)

[elsa-ite]: http://goto.ucsd.edu:8095/index.html#?demo=ite.lc

[elsa-not]: http://goto.ucsd.edu:8095/index.html#?demo=permalink%2F1491005489_149.lc
