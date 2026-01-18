# The Bisection Method

The Bisection Method is the canonical example of a bracketing method. Assuming that a function $f(x)$ is continuous and that precisely one root exists in a search range $x_L\rightarrow x_U$, it iteratively halves the size of the search range until we say "good enough". So: we might start the search knowing the root is between 0 and 100, a range of 100; after one iteration, we will be able to halve that to 50, after two iterations, 25, ... , after six iterations, we can say with confidence that the root lies within a range of 0.78125. Another way to say that: we pinpoint the root to $x_\text{root}\pm 0.390625$.

:::{note}
Throughout this class, we will often sketch out functions to try to explain/understand algorithms. However, it is usually the case that we don't actually know what the function looks like... otherwise we'd just say "the root is right there!"
:::

## The algorithm

0. For a given function $f(x)$, we define a search region between $x_L$ ("$x$ lower") and $x_U$ ("$x$ upper"). There must be precisely one root on this range, else the algorithm breaks!
1. Calculate $x_M$ ("$x$ middle") as $(x_L+x_U)/2$.
2. Calculate $f(x_L)$, $f(x_M)$, and $f(x_U)$ and consider the sign of $f(x_L)\cdot f(x_M)$ OR $f(x_M)\cdot f(x_U)$. (See discussion below about making your code more robust.)
3. (a) If $f(x_L)\cdot f(x_M)< 0$, that means that the function changes sign somewhere between $x_L$ and $x_M$. That is, the root is between $x_L$ and $x_M$