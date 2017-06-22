## Boolean Algebra and Operators
Boolean algebra is a branch of algebra where the values of variables can only be `true` or `false` (often denoted by `1` and `0` respectfully). We use boolean algebra in circuits, general two-valued logic (such as in mathematics), and boolean operations.


There are multiple operations in boolean algebra, but the ones we will focus on are `AND` and `OR`. We denote `AND` through multiplication (ex: `AB`) and we denote `OR` through addition (ex: `A+B`). These operations follow the commutative property, meaning that the order in which we place the operands does not matter.

## Truth Tables
Whenever we have a boolean expression, we can express it as a function. Similar to `F(x)` we can express a two variable function: `F(AB)`, where we can say our domain is `{A,B}`. Since our input values can only be `true` or `false`, we can create a truth table that will show all possible cases with their inputs to the function and the result. Let's take a look at a simple two variable expression, and see how the logic gates `AND` and `OR` work. 

For example, let's take the equation `F(AB) = AB` and generate the truth table: 

| F(AB)| A | B |
| ---- |:-:| -:|
| 0    | 0 | 0 |
| 0    | 0 | 1 |
| 0    | 1 | 0 |
| 1    | 1 | 1 |

We can also take the equation `F(AB) = A+B` and generate the truth table:

| F(A+B)| A | B |
| ----- |:-:| -:|
| 0     | 0 | 0 |
| 1     | 0 | 1 |
| 1     | 1 | 0 |
| 1     | 1 | 1 |

Truth tables are important because we can easily evaluate for the behavior of a function. For user input, it is easier to input truth-tables because we can specify cases such as `Don't Cares`, which will be discussed later on.

## Sum of Product Expressions (SOP)
Let's consider a more complicated expression `F(ABCD)= AB'C+BD+CD+D` and generate its truth table:

| F(AB'C+BD+CD+D)| A | B | C | D |
| ----- |:-:| -:| -:| -:|
| 0     | 0 | 0 | 0 | 0 |
| 1     | 0 | 0 | 0 | 1 |
| 0     | 0 | 0 | 1 | 0 |
| 1     | 0 | 0 | 1 | 1 |
| 0     | 0 | 1 | 0 | 0 |
| 1     | 0 | 1 | 0 | 1 |
| 0     | 0 | 1 | 1 | 0 |
| 1     | 0 | 1 | 1 | 1 |
| 0     | 1 | 0 | 0 | 0 |
| 1     | 1 | 0 | 0 | 1 |
| 0     | 1 | 0 | 1 | 0 |
| 1     | 1 | 0 | 1 | 1 |
| 1     | 1 | 1 | 0 | 0 |
| 1     | 1 | 1 | 0 | 1 |
| 0     | 1 | 1 | 1 | 0 |
| 1     | 1 | 1 | 1 | 1 |

This example was definately more involved than the previous expressions. An interesting observation is that we are doing a sum of product evaluation, that is, `AB'C+BD+CD+D` is a sum of products. The significance of a sum of product is that when we are doing `+` we are in fact invoking the `OR` operator. 

Moreover, the `OR` operator returns `true` so long as any one of its arguements returns `true`. Therefore, if _any_ of the terms in the sum of product (SOP) expressions is `true`, then we know that the final expression is `true` for certain.

## Example Algebraic Simplification

Let's simplify our expression from the previous truth table example. We can apply ordinary algebra tricks such as factoring. Remember that the `+` operator invokes the `OR` gate, and that `true or x` always returns `true` regardless of `x` (as shown in our first truth-table).
```
AB'C+BD+CD+D // Initial expression
AB'C+BD+D(C+1) // Factor out a D
AB'C+BD+D // Since (C+1) is always true, as C OR true is always true
AB'C+D(B+1) // Factor out a D again
AB'C+D // Since (B+1) is always true, as B OR true is always true
=AB'C+D // Final expression
```

As an exercise to the reader, complete the truth-table to show that they are logically equivalent. 

