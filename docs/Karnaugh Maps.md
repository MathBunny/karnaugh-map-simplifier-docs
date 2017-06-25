## Introduction
Karnaugh Maps are a way to visually display a boolean expression onto a 2D grid. We take the variables and bind them to an axis, and then enumerate through the possible combinations of input values that could occur for all those variables bounded to an axis (either horizontally or vertically).

For example, we can display the following 2 variable Karnaugh Map:

![](http://i.imgur.com/F4LfwMx.png)

We have bounded to the vertical axis, the variable `A`, and we enumerate through the possible values for `A` (being `{0, 1}`). Similarily, we perform a similar operation for the `B` variable. Since we are using a 2 variable expression, we can bound one variable to each axis and the visualization works fine in a `2x2` matrix.

Let's instead look at a more involved example with 4 variables:

![](http://i.imgur.com/7WaVxjX.png)

We have now bounded the `A` and `B` variables to the vertical axis, while we bounded the `C` and `D` variables to the horizontal axis. We now enumarate through different combinations of the bounded variables for each axis in *reflected binary code order* (more on this in the following section). Lastly, we indicate on the matrix each true value by augmenting a `1` value.

## Enumeration and Gray Codes
When enumerating through the variable input combinations for the binded axis, we take advantage of _reflected binary code order_, otherwise known as gray codes. If we observe carefully, we can notice that from one combination to another, we only vary by one bit. That is:

``` markdown
... 00 01 11 10 00 01 11 10 00 ...
    ^   ^ ^   ^ ^   ^ ^   ^ ^
```

Thus, we get this wrapping that allows us to switch by only one bit. This provides us the core for how Karnaugh Maps work.

## Groupings
The main idea for how Karnaugh Maps can be used to simplify expressions is to group pairs of `1` values that are adjacent, and exploit the fact that each one has only a bit difference from another. 

![](http://i.imgur.com/y3GDjr3.png)

For the purpose of this example, let `F(ABCD) = CELL`. We start with the expression `F(0000) = 1` and `F(0001) = 1`. However, notice that _regardless_ of the value of the last bit, we still get `1`. Hence, let's take a look at the SOP expressions:

```markdown
F(ABCD) = A'B'C'D' + A'B'C'D
F(0000) = 1
F(0001) = 1

Since the last bit is the same, we can ignore the D value, thus:
F(ABCD) = A'B'C'

We can confirm by simplifying algebraically:
F(ABCD) = A'B'C'D' + A'B'C'D
	    = A'B'C'(D' + D)
	    = A'B'C'
Therefore, the simplification is true.
```

We can then extend this rule to work for rectangles and more!