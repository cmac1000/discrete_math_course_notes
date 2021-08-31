# Problem 1

## 1a

```
Members(p, a, b) ::= ALL(z).(z IN p IFF (z = a OR z = b))
```
`Members(p, a, b)` is defined as the following set theory formula: For any element `z`, `z` is in the set `p` if and only if `z` is equal to set `A` or `z` is equal to set `B`.

## 1b

Note: it took me a minute to understand `pair(a,b) ::= {a{a,b}}`. I think I get it: because sets are unordered, we can use the "nestedness" of sets to reflect the ordering of a sequence. The "least nested" element of the set on the right side is the first element of the sequence, and the element appearing only in the "most nested" element of the set is the last element of the sequence. Pairs are just a special case of this.

```
Pair(p, a, b) ::= ALL(a), ALL(b).(Members(p, a, {a,b}))
```
`Pair(p, a, b)` is defined as the following formula: for any two elements, a and b, `Pair(p, a, b)` is true if and only if `a` and `{a,b}` are the only members of set `p`.

## 1c

```
Second(p, b) ::= SOME(a), ALL(b).(
    Pair(p, a, b)
)
```

`Second(p, b)`: for any `b`, there is some element `a` such that `Pair(p, a, b)` holds.

# Problem 2

Prove 

```
Complement(A & B) = Complement(A) | Complement(B)
```

Proof.

```
Complement(A & B) = Complement(A) | Complement(B)
```

is equivalent to 

```
z IN Complement(A & B) iff z IN (Complement(A) | Complement(B))
```

```
z IN Complement(A & B)
```

implies that 

```
NOT(z IN A & B)
```

So we know that `z` can't be in both `A` and `B`, by the definition of intersections:

```
NOT(z IN A AND z IN B)
```

This implies that at least one of the following must be true: `z` is not in `A`, or `z` is not in `B`:

```
NOT(z IN A) OR NOT(z IN B)
```

By the definition of complements, we therefore know that

```
z IN Complement(A) OR z IN Complement(B)
```

By the definition of unions, this is equivalent to

```
z IN (Complement(A) | Complement(B))
```

QED.

# Problem 3

## 3a

Show that if languages R and S are concatenation-definable, then so is `R & S`

By the definition of concatenation-definability, a c-d language can be constructed by starting with finite languages and applying concat, union or complement operations a finite number of times. 

Therefore, if we can make `R` and `S` in this manner, we can also make `R & S` by extending the operations count by one (adding one more union operation).

## 3b

Show that `0B1` is c-d.

Well, we know that `{0}` and `{1}` are both c-d because they are finite. And we also know that `B` is c-d, so `0B1` is a concatenation of three c-d languages, therefore it itself if c-d.

## 3c

Show that `0*` is c-d.

This can be expressed as the inverse of a c-d language, namely `B1B` - the language in which each word has a 1 in it somewhere. Inverse is an allowed operation for defining c-d languages, so `0*` is c-d.

## 3d

Show that `{0,1}*` is c-d.

This is the same as `B`, right? We can use the same logic as was used to show that `B` is c-d.

Let `u` = 10
Let `v` = 100
empty set is `{u} & {v}`, and complement of empty set is equivalent to `{0,1}*`

Therefore, `{0,1}*` is c-d.

## 3e

Explain why `{00}*` is not boring.

(`boring(S)` means either `S` or `complement(S)` is 0-finite - contains a finite number of words consisting entirely of 0s)

Let's see here. For `{00}*` to be non-boring, either the langage or its complement must not be 0-finite.

`{00}* & {0}*` is infinite
or
`complement({00}*) & {0}*` is infinite

`{00}*` contains `{00, 0000, 000000, 00000000, ...}` - an infinite set of all-0 words, so "`{00}* & {0}*` is infinite" is true.

`complement({00}*)` is the set of all binary words that can't be made by concatenating `00`s. This contains the set `{0}* - {00}*`, or all odd-digit all-0 words. This is also an infinite set of all-0 words, so "`complement({00}*) & {0}*` is infinite" is true.

Therefore `{00}*` is not boring.