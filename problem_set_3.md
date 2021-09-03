# problem 1

Using strong induction, prove that F(n), where F is fibonnaci function, is equivalent to 

    (p**n - q**n)/sqrt(5)

where

    p = (1 + sqrt(5))/2
    q = (1 - sqrt(5))/2

Proof. The proof uses strong induction.

Predicate:

Where `F(n)` is the Fibonnaci function,

    P(n) ::= (((1 + sqrt(5))/2)**n - ((1 - sqrt(5))/2))**n)/sqrt(5) = F(n)

For every non-negative integer `n`.

Base Case:

`F(0)` is 0.

    (((1 + sqrt(5))/2)**0 - ((1 - sqrt(5))/2))**0)/sqrt(5) = 
    (1 - 1)/sqrt(5) =
    0/sqrt(5) =
    0

Therefore `P(0)` is true.

NOTE: need to do 1 too maybe manually

Inductive Step:

Assuming that `P(0), P(1)...P(n)` is true, we prove that `P(n+1)` is true.

`(((1 + sqrt(5))/2)**0 - ((1 - sqrt(5))/2))**0)/sqrt(5) = F(n)`

I can reduce the problem to needing to prove the following:

`p**(n+1) = p**n + p**(n-1)`

The hint that `p**2 = p + 1` seems relevant here...

An interesting consequence of `p**2 = p+1` is that `p**n = F(n) + F(n-1)` I'm not sure I can prove that, but that's what I see.

Let's take that as a conjecture for now.

NOTE might need to prove this conjecture more properly.

---
## conjecture 1a

If `x` is one of `(1 + sqrt(5))/2` or `(1 - sqrt(5))/2`:

    x**n = x(F(n)) + F(n-1)

---

So, the proof looks like this:

    (p**n+1 - q**n+1)/sqrt(5) = F(n+1)

iff
    
    (p**n+1 - q**n+1)/sqrt(5) = F(n) + F(n-1)

because we already know that the relationship holds for `0..n`, we can rewrite as follows

    (p**n+1 - q**n+1)/sqrt(5) = (p**n - q**n)/sqrt(5) + (p**n-1 - q**n-1)/sqrt(5)

multiplying both sides of the equation of `sqrt(5)` yields

    p**n+1 - q**n+1 = p**n - q**n + p**n-1 - q**n-1

logically, this is the same as proving both

    p**n+1 = p**n + p**n-1
    q**n+1 = q**n + q**n-1

because conjecture 1a applies to both `p` and `q`, we can use the same logic for either, here denoted `x`:

    x**n+1 = x**n + x**n-1

by conjecture 1a:

    x(F(n+1)) + F(n) = x(F(n)) + F(n-1) + x(F(n-1)) + F(n-2)

by the definition of `F`:

    x(F(n)) + x(F(n-1)) + F(n) = x(F(n)) + F(n-1) + x(F(n-1)) + F(n-2)

subtracting common terms:

    F(n) = F(n-1) + F(n-2)

this is the definition of the `F` function, so it's true by definition. Thus, `(p**n+1 - q**n+1)/sqrt(5) = F(n+1)` is true. QED.
