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

1.) We can replace a leaf node on the `n`-leafed LBT with an internal node, which has two leaf node children. In this case, we remove a leaf node, add an internal leaf node, and add two leaf nodes, for a net gain of one leaf node and one internal node.
2.) We can "insert" an internal node between two existing nodes. If `B` is a child of `A`, and both are LBTs, we can insert `C` such that `C` becomes the child of `A`, and `B` becomes one child of `C`. To fulfil the definition of the `<l, B, C>` form, `C` needs another child, so we add a leaf node child. In this case, we add one internal node and one leaf node.

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
