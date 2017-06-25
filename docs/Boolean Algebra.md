## Boolean Algebra and Operators
Boolean algebra is a branch of algebra where the values of variables can only be `true` or `false` (often denoted by `1` and `0` respectfully). We use boolean algebra in circuits, general two-valued logic (such as in mathematics), and boolean operations.


There are multiple operations in boolean algebra, but the ones we will focus on are `AND` and `OR`. We denote `AND` through multiplication (ex: `AB`) and we denote `OR` through addition (ex: `A+B`). These operations follow the commutative property, meaning that the order in which we place the operands does not matter. We also have `NOT`, denoted by `'` operator, which flips the sign, for example `A'`.

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

Truth tables are important because we can easily evaluate for the behavior of a function. For user input, it is easier to input truth tables because we can specify cases such as `Don't Cares`, which will be discussed later on. 

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

Let's simplify our expression from the previous truth table example. We can apply ordinary algebra tricks such as factoring. Remember that the `+` operator invokes the `OR` gate, and that `true or x` always returns `true` regardless of `x` (as shown in our first truth table).
```
AB'C+BD+CD+D // Initial expression
AB'C+BD+D(C+1) // Factor out a D
AB'C+BD+D // Since (C+1) is always true, as C OR true is always true
AB'C+D(B+1) // Factor out a D again
AB'C+D // Since (B+1) is always true, as B OR true is always true
=AB'C+D // Final expression
```

As an exercise to the reader, complete the truth table to show that they are logically equivalent. 

## Undefined Input & Don't Cares
The definition of a "Don't care" is a combination of input values that is not known, and could be either `0` or `1`. For the purposes of variable simplification, we would choose the greedy approach of picking between {`0`, `1`} such that the simplified expression has less terms.

Let's consider the following truth-table:

| F(AB)| A | B |
| ---- |:-:| -:|
| 1    | 0 | 0 |
| 1    | 0 | 1 |
| ?    | 1 | 0 |
| 1    | 1 | 1 |

We observe that we have a _Don't care_. Let's observe the differences in cases for `F(1,0)`:

```markdown
Case #1: F(1, 0) = 0
=> F(AB) = A'B' + A'B + AB

Case #2: F(1, 0) = 1
=> F(AB) = A'B' + A'B + AB' + AB

Simplifying the cases...
F(AB) = A'B' + A'B + AB
	  = A'(B' + B) + AB
	  = A' + AB
F(AB) = A'B' + A'B + AB' + AB
	  = A'(B' + B) + A (B' + B)
	  = A' + A
	  = 1
```

We can clearly see, if we set `F(1, 0) = 1`, we get a true value for any input. Therefore, for the purposes of variable simplification, we can simply let `F(1, 0) = 1` thus implying `F(AB) = 1`.

## Additional Logic Gates
So far we covered the `NOT` unary operator, in addition to the binary operators `OR` and `AND`. 

![alt text](http://i.imgur.com/M59IOZQ.jpg"Logo Title Text 1")