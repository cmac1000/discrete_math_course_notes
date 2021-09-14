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

Update: this is incorrect, we're trying to find the intersection of R and S, not the union.

## 3b

Show that `0B1` is c-d.

Well, we know that `{0}` and `{1}` are both c-d because they are finite. And we also know that `B` is c-d, so `0B1` is a concatenation of three c-d languages, therefore it itself if c-d.

## 3c

Show that `0*` is c-d.

This can be expressed as the complement of a c-d language, namely `B1B` - the language in which each word has a 1 in it somewhere. Complement is an allowed operation for defining c-d languages, so `0*` is c-d.

## 3d

Show that `{0,1}*` is c-d.

This is the same as `B`, right? We can use the same logic as was used to show that `B` is c-d.

* Let `u` = 10
* Let `v` = 100
* empty set is `{u} & {v}`, and complement of empty set is equivalent to `{0,1}*`

Therefore, `{0,1}*` is c-d.

Update: this is incorrect, we want `{01}*`, not `{0,1}*`

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

## 3f

Verify that if `R` and `S` are boring, so is `R | S`

The union of two sets is every element that is in either set. "Boring" means that either that the language, or its complement, has finite `0` words.

If `R` and `S` are both 0-finite, then the union must be finite too - you can't get an infinite set by combining two finite sets.

Update: this step is invalid.

If both `R` and `S` are 0-infinite, this implies that both `complement(R)` and `complement(S)` are 0-finite. `R | S` in this case is 0-infinite, so we must demonstrate that `complement(R | S)` is 0-finite. By DeMorgan's law, this is equivalent to `complement(R) & complement(S)`. It's impossible for the intersection of two sets to be 0-infinite unless both are 0-infinite, so `complement(R) & complement(S)` is 0-finite, therefore `complement(R | S)` is 0-finite, therefore `R | S` is boring.

If `R` is 0-finite and `S` is not, then `complement(S)` must be 0-finite, because we know `S` is boring. `R | S` in this case is not 0-finite, because it contains the infinite `0`-words from `S`, so we must demonstrate that `complement(R | S)` is 0-finite.

If a language is 0-finite, its complement must be 0-infinite: there's an infinite set of `0` words in `{0}*`, so a finite subset can't subtract enough to prevent the remainder from staying infinite, in the complement.

Therefore, in this case, we know that `R` is 0-finite, `complement(R)` is 0-infinite, `S` is 0-infinite, and `complement(S)` is 0-finite.

Let's say in this case that `complement(R | S)` is 0-infinite.By DeMorgan's law, this is equivalent to `complement(R) & complement(S)`.

We know that `complement(S)` is 0-finite, and `complement(R)` is 0-infinite. It's impossible for the intersection of two sets to be 0-infinite unless both are 0-infinite, so this is impossible.

Therefore, `complement(R | S)` is 0-finite, and therefore `R | S` is boring.

This works symmetrically if `R` is 0-infinite and `S` is 0-finite.

## 3g

Verify that if `R` and `S` are boring, then so is the cartesian product of `R` and `S`.

The proof is by cases. There are three possible cases:

1. both `R` and `S` are 0-finite.
2. `R` or `S` contain no `0`-words at all, including the empty word.
3. at least one of `R` or `S` is 0-infinite, and both contain `0` words.

### 1

If both `R` and `S` are 0-finite, then the cartesian product `R ⋅ S` is boring.

We can prove this by proving that `R ⋅ S` is 0-finite.

Proof. The proof is by contradiction. Let's assume that `R ⋅ S` is 0-infinite, that is `(R ⋅ S) & {0}*` is an infinite set.

We can define two new languages: `A ::= (R & {0}*)` and `B ::== (S & {0}*)`. That is, `A` is the set of `0` words in `R` and `B` is the set of 0-words in `S`. Because `R` and `S` are both 0-finite, `A` and `B` are both finite sets.

Logically, `(R ⋅ S) & {0}*` is equivalent to `A ⋅ B`: there's no way to make 0-words in `R ⋅ S` that are not in `A ⋅ B`, and there are no words in `A ⋅ B` that are not in `(R ⋅ S) & {0}*`.

By assumption, `(R ⋅ S) & {0}*` is infinite, but this implies that the cartesian product of two finite sets is an infinite set. This is a contradiction, so `(R ⋅ S) & {0}*` is finite, therefore `R ⋅ S` is 0-finite, therefore `R ⋅ S` is boring in this case. QED.

### 2

If `R` or `S` contain no `0`-words at all, including the empty word, then `R ⋅ S` is boring.

Proof.

In this case, `(R ⋅ S) & {0}*` is the empty set: there is no way to make 0-words in `R ⋅ S` unless both `R` and `S` contain 0-words. Therefore, there is a finite number (0) of 0-words in `R ⋅ S`, therefore `R ⋅ S` is boring in this case. QED.

### 3

If `R` and `S` are boring, at least one of `R` or `S` is 0-infinite, and both contain `0` words, then `R ⋅ S` is boring.

In this case, `R ⋅ S` is 0-infinite, because you can join an infinite series of 0-words from one language with at least one 0-word from the other.

Therefore, we must prove that `complement(R ⋅ S)` is 0-finite.

There are two sub-cases here:

    a.) one of `R` and `S` is 0-finite, and the other is 0-infinite
    b.) `R` and `S` are both 0-infinite


#### 3a 

If `R` and `S` are boring, one of `R` and `S` is 0-finite, the other is 0-infinite, and both contain `0` words, then `complement(R ⋅ S)` is 0-finite.

So there must be a finite number of 0 words that can't be made by concatenating words in `R` and `S`.

That is, `complement(R ⋅ S) & {0}*` is finite.

Let's say that `R` is 0-finite, and `S` is 0-infinite, so `complement(R)` is 0-infinite and `complement(S)` is 0-finite. Both contain `0`-words, so their complements are not equivalent to `{0}*`.

///
Let's try a contradiction.

Assume that `complement(R ⋅ S) & {0}*` is infinite.

This means that there is an infinite set of 0-words that can't be made by concatenating words in `R` and `S`.

We know that `R ⋅ S` is 0-infinite.


We know about S:

* it's 0-infinite
* its complement is 0-finite.

....

#### 3b

If `R` and `S` are boring, and `R` and `S` are both 0-infinite, then `complement(R ⋅ S)` is 0-finite.

In this case, `complement(R)` and `complement(S)` are both 0-finite.

## 3h

Explain why all c-d languages are boring.

c-d means that the language can be constructed by starting with finite languages and applying union/concat/complement a finite number of times.

boring means the language or its complement are 0-finite.

So, we're saying that for every language that is constructed from finite languages and finite union/concat/complement, that language or its complement are 0-finite.

Well, let's take the contradiction. Say there's a c-d language `M` that is 0-infinite, and its complement is 0-infinite as well.

We know that to construct this language we started with finite languages, and applied some number of union/concat/complements to them.

Finite languages are boring by definition, so there must have been some step at which either a union, concat or complement operation was applied to boring languages to create a non-boring language. Let's call this step the "magic step".

So there are three cases to consider:

1. the magic step was a union operation
2. the magic step was a complement operation
3. the magic step was a concat operation

Case 1 is ruled out by the proof above (problem 3f) that the union of any two boring languages is boring.

Case 2 is ruled out because `complement(A)` of a boring language must be boring. Let's call the complement of `A` in this case `B`. Because `A` is boring, we know that either `A` or `complement(A)` is 0-finite. If `A` is 0-finite, `complement(B)` will be 0-finite, making `B` boring. Conversely, if `complement(A)` is 0-finite, `B` will be 0-finite, making `B` boring. This covers all cases, so Case 2 is impossible.

The concatenation of two langauges is a cartesian product, so case 3 is ruled out by the proof above (3g) that the cartesian product of any two boring languages is boring.

This covers all cases, so there is no magic step. This is a contradiction, so the langage `M` does not exist. Therefore, all c-d languages are boring. QED.