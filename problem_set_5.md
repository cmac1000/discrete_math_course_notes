# problem 2

## 2a

    u <-> w <-> v

There's a path (`u->w->v`) from `u` to `v`, and one (`v->w->u`) from `v` to `u`.

However, attempting to make a cycle out of these two paths fails, because a cycle requires that walk's vertices be distinct except for beginning and end. A walk like `u->w->v->w->u` is a closed walk, but it's not a cycle, because it passes through `w` twice.

## 2b

Proposition: If a digraph has a positive-length closed walk beginning and ending at vertex `v`, it also contains a cycle that contains `v`.

We know that there is a positive length closed walk beginning and ending at `v`. That means that there must be at least two paths involving `v`:

    v->x
    y->v

Where `x` and `y` are other vertices in the digraph. `x` and `y` may be identical to each other, or may be distinct; but neither may be identical with `v`.

We also know that there must be a walk from `x` to `y`, which has a length of 0 or more.

If the walk from `x` to `y` has length 0, `x` and `y` are the same vertex. In this case, `v->x->v` is a cycle, and the proposition is true.

If the walk from `x` to `y` is positive, there are two subcases:

**The walk is a path**, that is it contains no repeated vertices. In that case, `v->x->{x-to-y path}->y->v` is a cycle, and the proposition is true.

**The walk is not a path**, that is it contains repeated vertices. In that case, there must be a first repeated vertex, when following the path from `x` to `y`, call it `z`. So the path is something like `v->x->{x-to-z path}->z->{more vertices}->z->{z-to-y path}->y->v`. This is not a cycle, because `z` repeats, but because there's a path from `x` to `z`, and from `z` to `y`, we can "cut off" the parts of that path after `z`, and get `v->x->{x-to-z path}->z->{z-to-y path}->y->v`. This is a cycle, and thus the proposition is true.

Because the proposition is true in all case, it is proved. QED.

# problem 3

