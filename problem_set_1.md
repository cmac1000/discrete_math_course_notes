# problem 1

Prove that `log(6, 4)` is irrational (logarithm of 6 base 4).

## Solution

Proof. The proof is by contradiction.

Assume that `log(6, 4)` is rational. This means that there is a ratio, `m/n`, such that `4**(m/n)=6`, and `m` and `n` are integers that share no common factors.

`log(6, 4)`

implies that

`4**m == 6**n`

which, when factored down to primes, yields the equivalent

`2**2m == 3**b * 2**b`

But this requires that a power of 3 is equivalent to a power of 2. By the unique factorization theorem, this is impossible. This is a contradiction. QED.

## Thinking

It seems like you want to do this by contradiction, something like this:

Proof. The proof is by contradiction.

Assume that `log(6, 4)` is rational. This means that there is a ratio, `m/n`, such that `4**(m/n)=6`, and `m` and `n` are integers that share no common factors.

Some equivalent statments:

* the `m/n`th root of 6 is 4
* the nth root of `4**m` is 6
* `4**m=6**n`

6 and 4 share a common factor, 2, but that doesn't get us anywhere obvious - the logarithm of 64 base 4 is 3, which is rational, and 64 and 4 share common factors. `m` and `n` could be arbitrarily large, so we can't say anything about them by exhaustive search.

~~The well-ordering principle might be useful here. If `X` is the set of satisfying ratios for `m/n`, there must be a smallest member of X, `x`. If we can show that `x` could in fact be written in lower terms, we've shown a contradiction and we're done.~~

Ah, but we can't do that with rationals, the WOP doesn't apply to rationals, because you can always multiply to get a smaller one. It does apply to the integers comprising the rational `m/n`.

So you could say that `M` is the set of integers that would satisfy the numerator in `m/n`, and `N` the set of denominators. So in lowest terms, `m` is the smallest member of M and `n` is the smallest member of `N`. WOP applies to both these sets, so you could demonstrate a contradiction by showing:

* the lowest `m` must share a common factor with the lowest `n`

A pattern I notice in logarithms that do have rational solutions is that either the base is a factor of the anti-logarithm, in the case of logarithms greater than 1, or the anti-logarithm is a factor of the base, in the case of logarithms smaller than 1. For example:

```
log(64, 4) = 3
```

```
log(2, 4) = 1/2
```

But this relationship doesn't seem to hold up for 10,2 or 6,3, so it can't be all there is to it.

Ok, it's not just that one is a factor of the other, it's that one to the power of an integer equals the other.

So

```
log(4,64) = 1/3
```

This seems like an important relationship, core to the behavior of logarithms. If I could just assume it as an axiom, I'd be done, because it's easy to show that there's no integer x such that `6**x=4` or `y` such that `4**y=6`

But I don't know enough to assume it as an axiom, because this pattern only covers integer logarithms, or logarithms of the form `1/integer` - it's possible that `2/3` is a valid logarithm of some anti-logarithm and some base.

~~But maybe I can conclude that this covers all cases, and 2/3 is never a valid logarithm. Circumstancially, that seems true: `[x**(2/3) for x in range(2,100)]` produces no integers.~~

Ah, but actually I think we have one. `log(4,8)` is `2/3`, I believe. But usefully, this is another logarithm where one term is a factor of the other.

So I haven't found any counterexample to the conjecture:

For every rational logarithm, either the base is a factor of the anti-logarithm, or the anti-logarithm is a factor of the base.

But that's not the same as a proof, so this isn't strong enough to use as an axiom to prove our original proposition.

### note after reading stack overflow:

I think the conjecture above is a restatement is the theorem of unique prime factorization (or at least a consequence of it)

```python
>>> [print('log({},{})'.format(round(x**(2/3)), x)) for x in [x for x in range(2,1000) if abs(x**(2/3) - round(x**(2/3))) < 0.0000000001]]
```

so these are all `2/3`:

```
log(4,8)
log(9,27)
log(16,64)
log(25,125)
log(36,216)
log(49,343)
log(64,512)
log(81,729)
```

factor pattern holds

these are `3/5`:

```
log(8,32)
log(27,243)
```

this is `4/9`:

```
log(16,512)
```

I read some stackoverflow, and the key here is unique prime factorization: https://math.stackexchange.com/a/1416229

# problem 2

Use WOP to prove that `n <= 3**(n/3)` for all non-negative integers.

## Thinking

The proof is by contradiction.

Let `C` be the set of all non-negative integers `n` for which

`n > 3**(n/3)`

By the well-ordering principle, there must be a smallest integer, `c` in `C`.

We can calculate that `c` is greater than 4:

```python
>>> any([x > 3**(x/3) for x in [0,1,2,3,4]])
False
```

Equivalent statements:

* `n > cuberoot(3**n)`
* `n**3 > 3**n`

We know that `n/3 > 1`, because we've calculated all possible integers less than 4.

A rough attempt:

For each integer `n` counting up from 4, the left side of the inequality grows linearly, by 1.

For the inequality to ever hold, the right side of the inequality would have to grow sub-linearly. But it increases exponentially, once the exponent is greater than 1. The smallest `c` would have to come before `n/3` is greater than one, to avoid this exponential trap, and we've seen by calculation that it does not.

Therefore, there is no smallest `c` in `C`, `C` is an empty set, and the proposition is proved. QED.

# problem 3a

`(P IMPLIES Q) OR (Q IMPLIES P)`

P | Q | P IMPLIES Q | Q IMPLIES P | CENTRAL OR
---
T | T |      T      |      T      |      T
T | F |      F      |      T      |      T
F | T |      T      |      F      |      T
F | F |      T      |      T      |      T

# 3b

```
(P IMPLIES Q) AND (Q IMPLIES P)
```

would do it but we can't use implies

```
(NOT(NOT(P) AND Q)) AND (NOT(NOT(Q) AND P))
```

# 3c

`P is valid iff NOT(P) is not satisfiable`

because if there is a valid environment that makes `NOT(P)` true, it means that `P` is not true in every environment, which is the definition of validity.

# 3d

`P AND NOT(Q)`

# Problem 4.a

```
p0 = NOT(a0)
c = a0
```

# 4.b