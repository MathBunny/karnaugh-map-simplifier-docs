# Algorithm Overview
The process of simplifying variables essentially involves greedily obtaining larger rectangles to encompass as many `1` unit within a grid. To ensure that we cover all the possible pairings, we need to devise an algorithm to generate a sample space containing all possible outcomes, and then we can pick out the pairings that we need from there.

The process begins by plotting the points `0` and `1` in the Karnaugh Map. We can assume that the up left corner in `(x,y)` coordinate is `(a,b)` and bottom right corner is `(c,d)`. An interesting property is that:

> Consider the grouping `(a,b)` to `(c,d)`. The group is valid if and only if sum of all `1`s in the rectangle is equal to `(c-a)*(d-b)`.

The significance of this property is that we can quickly identify if a grouping is valid or not in `O(1)` time. Thus, we can exhaust all possible scenarios and we saved a linear (or quadratic) factor.

## Fundamental Theorem of Calculus
The first part of the fundamental theorem of calculus claims that we can take the anti-derivative of a function `ƒ`, and find the area under the curve from point `A` to `B` by doing `F(A)-F(B)`. Extending this definition to arrays, we can generate an anti-derivative for an array and find the summation from point `A` to `B` in `O(1)` time.

Consider:
```
arr = [1, 0, 1, 1, 0, 1]
arr* = [0, 1, 1, 2, 3, 3, 4]
```

We can then find the summation from item `arr[i]` for `i = [a, b]` by doing:
```
sum = arr*[b+1] - arr*[a];
```
This alow us to sum up values very quickly, and extending this to two dimensions we can rule out impossible cases.

Remark: Notice the length of the array is one index larger.

## Principle of Inclusion-Exclusion
Due to the nature of Karnaugh Maps, we would want to be able to do summation in two dimensions. This can be achieved using the principle of inclusion-exclusion. 

Applying the exact same algorithm as before, except now the size of the array is one larger on the horizontal axis and one larger on the vertical access as well. 

The final formula for retrieving the area is:
```
sum = arr*[d+1][c+1] - arr*[d+1][c] - arr*[d][c+1] + arr*[b][a];
```

## Priority Groupings + Heuristic
Generating valid groupings becomes trivial upon being able to check the validity using 2D prefix sum arrays. Iterate through all the `(x,y)` pairs, then try all possible starting and ending coordinates. This operation will take `O((NM)^2)`, where `N` = # of rows, `M` = # of columns.

When deciding the final groupings, insert all of the candidate groupings as an encapsulated object into a priority queue. The key in the priority queue used will be the size of the grouping. If two groupings are equal in size, the one with the more "square" shape will get a higher priority. The method for determining the "square-ness" of a candidate is the absolute difference in its width and height.

## Approach Drawbacks

The first drawback for this approach is speed. Despite being able to eliminate all solutions that don't satisfy the rectangular property of a grouping in `O(1)` time, we still exhaust all possibilities. Moreover, we also store the entire solution space in a priority queue which is very memory intensive.

## Memory Optimization: Cell-Wise Priority Queues

An important observation to make is that we are only interested in the largest possible grouping from each particular cell. This means that during each iteration of the algorithm, we should have at most `NxM` items in our priority queue, because the rest aren't useful! We can extend this idea by simply have a cell-wise 2D array that represents the grid used by cell, that is, a grouping that warrants its existence because it is the largest grouping to satisfy a given cell.

This however adds a factor of time complexity, how do we know that a rectangular grouping is a maximum for any of the cells within the area it surrounds? One approach is to manually check each cell, but it isn't good because it takes `NxM` amount of time. 

Another approach is to ...  coming soon!

 