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

`a` and `c` both move up the x-axis, so once the robot passes 1 on the x-axis, he can never return, and thus can never make it to (1,1). `a` can't be the beginning move of a successful sequence, because it immediately moves to 2 on the x-axis, and we already know there's no going back.

`c` also fails as the beginning move of a successful sequence: from (1,3) either `a` or `c` will carry the robot further up the x-axis with no return.

Therefore, we can eliminate sequences from `{a,c}*`

# {b,c}*

`b` and `c` have an analagous problem, moving continually up the y-axis. We can employ similar logic here to disqualify both as starting moves:

`c` is unworkable as an opening move, immediately moving the robot to 3 on the y-axis, whence no return.

`b` fails as well: from the opening move (0,0) -> (-2, 1), there's no way to stay on or return to y-axis 1. Either `b` or `c` as the second move moves the robot too far up the y-axis, doomed to wander eternally north.

Having eliminated all move sequences that could possibly advance, we conclude that the set of moves sequences ending in (1,1) is empty. QED.

# problem 2