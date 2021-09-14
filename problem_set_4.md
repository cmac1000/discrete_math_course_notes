# problem 1

For the robot to ever make it to (1,1) there would have to be a sequence of the following moves ending on (1,1) from the origin (0,0):

    a. (+2,-1)
    b. (-2,+1)
    c. (+1,+3)
    d. (-1,-3)

`a` and `b` are inverse operations, as are `c` and `d`. Any sequence containing an operation and its inverse can be simplified by removing both, so we can ignore any sequences that contain both `a`s and `b`s, or both `c`s and `d`s. That means there are four possible sets of sequences that are worth considering:

    {a,c}*
    {a,d}*
    {b,c}*
    {b,d}*

We can eliminate `{a,d}*` and `{b,d}*` with the observation that `a` and `d` both move down the y-axis, and both `b` and `d` move down the x-axis. Any sequence of steps leading to (1,1) must at some point enter the positive quadrant, and sets consisting of these moves are unable to do so.

This leaves two more interesting cases:

# {a,c}*

There must be a first move in any successful sequence. If we can eliminate `a` and `c` from being viable first moves, we can eliminate `{a,c}*`.

`a` and `c` both move up the x-axis, so once the robot passes 1 on the x-axis, he can never return, and thus can never make it to (1,1). `a` can't be the beginning move of a successful sequence, because it immediately moves to 2 on the x-axis, and we already know there's no going back.

`c` also fails as the beginning move of a successful sequence: from (1,3) either `a` or `c` will carry the robot further up the x-axis with no return.

Therefore, we can eliminate sequences from `{a,c}*`

# {b,c}*

`b` and `c` have an analagous problem, moving continually up the y-axis. We can employ similar logic here to disqualify both as starting moves:

`c` is unworkable as an opening move, immediately moving the robot to 3 on the y-axis, whence no return.

`b` fails as well: from the opening move (0,0) -> (-2, 1), there's no way to stay on or return to y-axis 1. Either `b` or `c` as the second move moves the robot too far up the y-axis, doomed to wander eternally north.

Having eliminated all move sequences that could possibly advance, we conclude that the set of moves sequences ending in (1,1) is empty. QED.

# problem 2

Proof. The proof is by structural induction.

The induction hypothesis is:

    P(n) ::= for every uniquely-labeled LBT B with n leaf nodes,
             fB = nB + 1

    where

    fB ::= distinct leaf label count of B
    nB ::= distinct internal label count of B

Base case (`n=1`):

There's only one possible LBT with leaf count 1, `<l, leaf>`. This has one distinct leaf label (`l`) and no internal labels, so

    fB = nB + 1
    1 = 0 + 1

Therefore the `P(1)` holds.

Constructor case:

Assuming `P(n)`, we must prove `P(n+1)`

The root of all LBTs with more than 1 leaf node is an LBT of the form `<l, B, C>`. Let's call this form an "internal node".

Let's call the form `<l, leaf>` a "leaf node".

Because we're dealing with uniquely-labelled LBTs, each internal node must have two unique child nodes, which can be either internal nodes or leaf nodes.

By assumption, `P(n)` is true: that means that there's a uniquely-labelled LBT with `n` nodes. There are two ways we can turn an LBT with `n` leaf nodes into an LBT with `n+1` leaf nodes:

1. We can replace a leaf node on the `n`-leafed LBT with an internal node, which has two leaf node children. In this case, we remove a leaf node, add an internal leaf node, and add two leaf nodes, for a net gain of one leaf node and one internal node.
2. We can "insert" an internal node between two existing nodes. If `B` is a child of `A`, and both are LBTs, we can insert `C` such that `C` becomes the child of `A`, and `B` becomes one child of `C`. To fulfil the definition of the `<l, B, C>` form, `C` needs another child, so we add a leaf node child. In this case, we add one internal node and one leaf node.

In both cases, we add one internal node and one leaf node, so

    Let fB(n) be fB for the n-leaf uniquely-labelled LBT
    Let nB(n) be nB for the n-leaf uniquely-labelled LBT
    Let fB(n+1) be fB for the n+1-leaf uniquely-labelled LBT
    Let nB(n+1) be nB for the n+1-leaf uniquely-labelled LBT

Because we always add one of each to create an `n+1`-leafed uniquely-labelled LBT:

    fB(n+1) = fB(n) + 1
    nB(n+1) = nB(n) + 1

So:

    fB(n) = fB(n+1) - 1
    nB(n) = nB(n+1) - 1q

By assumption,

    fB(n) = nB(n) + 1

Substituting:

    fB(n+1) - 1 = nB(n+1) - 1 + 1

Simplifying:

    fB(n+1) - 1 = nB(n+1)

Adding one to both sides:

    fB(n+1) = nB(n+1) + 1

This is the statement of `P(n+1)`, so we have proved that `P(n+1)` holds.

Therefore, `P(n)` holds for every uniquely-labelled LBT with `n` leaf nodes. QED.

# problem 3

## 3a

    f(x) := (1/x) - 1

is a bijection from (0,1] to [0, infinity) in the domain of real numbers

`1/x` almost works because it maps the uncountable set of irrational numbers between 0 and 1 to the uncountable set of irrational numbers between 0 and 1, and maps the rational numbers similarly.

But it fails to be a bijection because it leaves the 0..1 segment of the [0, infinity) interval empty. Subtracting by 1 solves this.

## 3b

I'm not sure how to do this one. Adding a leading decimal point to any sequence in `L` yields an irrational number between 0 and 1. This is an easy bijection between `L` and the irrationals. But, the unit interval includes rationals too, and that's harder.

Because sequences in `L` don't terminate, or end with infinite 0s, you can't get a rational by adding a leading decimal point to any sequence. So, for example, there's no sequence in `L` that will yield `1/2` when following the decimal point procedure, which means that the decimal point procedure doesn't yield the bijection we need.

`L` is an infinite set, which is presumably crucial to the trick here. You could do something like slice off the leading digit and use that as a flag, to switch between two different procedures, one of which would yield rational numbers somehow. 

Say you have these two members of L:

    A: 0 then infinite 1s
    B: infinite 1s

and your procedure is something like

    if the leading digit is 0, remove it and (somehow generate a rational number)
    else, follow decimal point procedure

then it would give you two infinite sets, those starting with 0 and all others.

Intuitively, this seems to break the bijection between irrational numbers and members of L. "0 then infinite 1s" corresponds to some irrational number, so hiving it off and hijacking it for our rational-number procedure means that that irrational number now has no arrow pointing to it, meaning our bijection is broken.

You could do a version where you always remove the first digit, but then "2, 0 then infinite 1s" and "3,0 then infinite ones" now point to the same irrational number, again breaking the bijection.

If there were some nonsense sequence of digits that we could turn into 0s, that would work - say "5 then (magic sequence)" would then become "5 then 0s", which gives us a rational. But logically, it seems like any identifiable sequence of digits would create a distinct irrational number, and we need all of those for the bijection to work.

I may be missing something basic, but I can't think of a way forward here.

## 3c

surjective func from `L` to `L**2` involving alternating digits

Ok, so let's say that `LA` and `LB` are both members of `L`.

So, the combination of those two yields `LC`, a member of `L**2`, which we can do by alternating the digits:

`LA0, LB0, LA1, LB1, LA2, LB2...`

But, since `L` is the set of all infinite sequences with infinite non-zeros, `LC` is also a member of `L`. In fact, every member of `L**2` is a member of `L`. Therefore, the identity function works as a surjection from `L` to `L**2`:

    f(x) = x

This doesn't seem to require the hint that the surjection need not be total, so maybe I'm missing something here.

## 3d

Lemma 3.1: if A and B are nonempty sets, and there is a bijection from A to B, then there is also a bijection between AxA and BxB (x means cartesian product)

This makes intuitive sense, I think it follows from the definition of a bijection.

any member of AxA is the combination of two members of A: A0 and A1.

similarly, any member of BxB is the combination of two members of B: B0 and B1.

let's call our A->B bijection `f`.

let's say that `f(A0) = B0` and `f(A1) = B1`. By the definition of bijections, no other values of `A` equal the corresponding `B` values.

So, it's simple to extend `f` to be a bijection between `AxA` and `BxB`:

    f(A0),f(A1) = B0, B1

the fact that `f` is a bijection guarantees that this generates a "unique address" in the codomain from all `AxA` to all `BxB` with no overlap.

///

Prove there is a bijection from `L**2` to `(0,1]**2`

We know (or are supposed to) from problem `b` that there is a bijection from `L` to `(0,1]*`. From lemma 3.1, it immediately follows that there is a bijection from `L**2` to `(0,1]**2`. QED.

# 3e

Prove a surjection from `(0,1]` to `(0,1]**2`

By problem c, we know that `L surj L**2`

Because problem b tells us that `L bij (0,1]`, we can substitute and get

`(0,1] surj L**2`

By lemma 3.1, it follows that `L**2 bij (0,1]**2`, so we can substitute again:

`(0,1] surj (0,1]**2`

Schröder-Bernstein says: for sets A,B; if A surj B and B surj A, then A bij B

It's easy to show that `(0,1]**2 surj (0,1]`: `f(x) = x[0]` is a surjective function from pairs of real numbers to real numbers.

Therefore, Schröder-Bernstein implies that `(0,1] bij (0,1]**2`

# 3f

Complete the proof that `(0,1] bij [0, infinity)**2`

Proof. The proof is by implication.

By problem a, we know that 

    3.1 (0,1] bij [0, infinity)

By problem d, this implies

    3.2 (0,1]**2 bij [0, infinity)**2

By problem e, we know that 

    3.3 (0,1] bij (0,1]**2

because of this bijection, we can rewrite 3.2 as

    3.4 (0,1] bij [0, infinity)**2

QED.