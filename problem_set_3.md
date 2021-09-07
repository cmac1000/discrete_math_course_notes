# problem 1

Using strong induction, prove that F(n), where F is fibonnaci function, is equivalent to 

    (p**n - q**n)/sqrt(5)

where

    p = (1 + sqrt(5))/2
    q = (1 - sqrt(5))/2

Proof. The proof uses strong induction.

Predicate:

Where `F(n)` is the Fibonnaci function,

    P(n) = (((1 + sqrt(5))/2)**n - ((1 - sqrt(5))/2))**n)/sqrt(5) = F(n)

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

An interesting consequence of `p**2 = p+1` is that `p**n = x(F(n)) + F(n-1)` I'm not sure I can prove that, but that's what I see.

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

# problem 2

```
    p(S) = k(k - 1)/2  # k is number of boxes in S
    p(A) = sum([p(s) for s in A])
```

Show that for any set of stacks `A`, if a sequence of moves starting with `A` leads to another set of stacks, `B`, then `p(A) >= p(B)`, and score for this sequence of moves is `p(A) - p(B)`.

## thinking

The proof uses induction.

Predicate:

For any number of moves `n` from set `A` to set `B` in the block-stacking game, let `P(n)` be the proposition that:

> a. the score for the sequence is `p(A) - p(B)` and
> b. `p(A) >= p(B)`

Base case:

If the number of moves from `A` to `B` is 0, then `A` and `B` are equivalent sets. Scores only come from making moves, so if there is no move, there is no score. If `A = B`, then `p(A) = p(B)`, and `x - x = 0` for any integer `x`, so part `a` of the predicate is true in this case.

`x >= x` is also true for any integer `x`, so part `b` of the predicate is also true.

Therefore, `P(0)` is true.

Let's also establish that for any single move from `A` to `B`, `p(A) - p(B) = score(move)`

Let's denote size of a stack as `s(S)`

We're making a move, so `s(A) > 1`. The move splits a stack in `A` into two stacks in `B`, call them `B0` and `B1`. The remaining elements of `A` are by the move, so they can be disregarded for the purposes of comparing `p(A)` and `p(B)`. To simplify, we can therefore assume that `A` contained a single stack `A0`, and `B` contains only `B0` and `B1`

So, we must prove that

    p(A) - p(B) = score(move)

By the definition of p(A) for sets, this is equivalent to:

    p(A0) - (p(B0) + p(B1)) = score(move)

By the scoring rules:

    p(A0) - (p(B0) + p(B1)) = s(B0)s(B1)

By the definition of p(S) for stacks:

    s(A0)(s(A0)-1)/2 - (s(B0)(s(B0)-1))/2 + (s(B1)(s(B1)-1))/2) = s(B0)s(B1)

To reduce the number of parens, let's define:

    z = s(A0)
    x = s(B0)
    y = s(B1)

so

    z(z-1)/2 - (x(x-1)/2 + y(y-1)/2) = xy

because `z = x + y`:

    (x + y)(x + y - 1)/2 - (x(x - 1)/2 + y(y - 1)/2) = xy

multiplying both sides by 2:

    (x + y)(x + y - 1) - (x(x - 1) + y(y - 1)) = 2xy

multiplying out the polynomials:

    x**2 + y**2 + 2xy + -x + -y + -x**2 + x + -y**2 + y = 2xy

simplifying:

    2xy = 2xy

this is true, therefore `p(A) - p(B) = score(move)` for any single move.

There's no way in the rules for a score to be negative, so this implies that `p(A) >= p(B)`. 

Therefore, `P(1)` is true.

Inductive step:

Assuming that `P(n)` is true, we prove that `P(n+1)` is true.

Let's start with part `a` of the predicate:

> the score for the sequence is `p(A) - p(B)`

