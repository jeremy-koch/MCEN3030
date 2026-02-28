# Golden Search

The Golden Search Method is a way to algorithmically find the maximum of a function $f(x)$ on a given range $x_L\rightarrow x_U$ with a minimum number of function evaluations. The idea is similar to [The Bisection Method](../3_root-finding/bisection.md): evaluate the function at a few locations, then deduce that the maximum cannot occur within a certain subset of the range, then reduce the range and redefine variables, then iterate until we are happy with the error bound.
:::{tip}
If a minimum is desired, we can either flip the logic described below, or just find the max of $-f(x)$.
:::

## The algorithm

We will use $d=(\sqrt{5}-1)/2\approx 0.618$ in the following. See below for why.

0\. For a given function $f(x)$, we define a search region between $x_L$ ("$x$ lower") and $x_U$ ("$x$ upper") for which we are seeking a maximum. The following presumes there is precisely one maximum on the range, however...

:::{note}
Unlike Bisection Method (with roots), this algorithm does not fail in the case that there are multiple local maximums in the search range -- it will find one of them. We just can't be confident that the local max that we find is the largest value on the search range.
:::

1\. Calculate two interior points: $x_2 = x_U - d(x_U-x_L)$ and $x_1 = x_L + d(x_U-x_L)$. Assuming that $x_L<x_U$, we will have $x_L<x_2<x_1<x_U$.  
2\. Calculate $f_1=f(x_1)$ and $f_2=f(x_2)$.



3\.  The path depends on the function values:  
(a) If $f(x_1)>f(x_2)$, the maximum cannot be between $x_L \rightarrow x_2$. We toss that range from our search and change values:

$$
x_L=x_2\\
x_2=x_1\\
f_2=f_1\\
x_1=x_L+d(x_U-x_L)
$$

and evaluate a new $f_1=f(x_1)$.

(b) If $f(x_2)>f(x_1)$, the maximum cannot be between $x_1 \rightarrow x_U$. We toss that range from our search and change values:

$$
x_U=x_1\\
x_1=x_2\\
f_1=f_2\\
x_2=x_U-d(x_U-x_L)
$$

and evaluate a new $f_2=f(x_2)$.
:::{hint}
When programming, it is important to change the values in this order. Do you see why?
:::

4\. Go back to step 3 and iterate until happy with the error bound.

## An example

The function $f(x)=\ln(x)\exp(-x)$ has one maximum between $x_L=0$ and $x_U=3$. Let's do a few iterations of the Golden Search Method.

### Iteration 1

We have $x_1=x_L+d(x_U-x_L) = 1.854$ and $x_2=x_U-d(x_U-x_L) = 1.146$, for which we evaluate $f_1=0.097$ and $f_2=0.043$. We notice that $f_1>f_2$, and so we toss $x_L\rightarrow x_2$ from our search.
:::{hint}
Another way to describe the logic: the max could occur left or right of $x_1$, corresponding to a negative or positive slope at $x_1$, respectively. But, assuming there is indeed only one max on this range, the slope at $x_2$ has to be positive, and so the root must be to the right of $x_2$
:::
Redefine:

$$
x_L=1.146~(\text{the old}~x_2)\\
x_2=1.854~(\text{the old}~x_1)\\
f_2=0.097~(\text{the old}~f_1)\\
x_1=1.146+d(3-1.146) = 2.292~(\text{note}~x_1>x_2)\\
f_1=0.084
$$

and we keep $x_U=3$.

### Iteration 2

Now we see $f_2>f_1$, and so we toss $x_1\rightarrow x_U$ from our search. Redefine:

$$
x_U=2.292~(\text{the old}~x_1)\\
x_1=1.854~(\text{the old}~x_2)\\
f_1=0.097~(\text{the old}~f_2)\\
x_2=2.292-d(2.292-1.146) = 1.584~(\text{note}~x_1>x_2)\\
f_2=0.094
$$

and we keep $x_L=1.146$.

### Iteration 3

Now $f_1>f_2$. What should we discard?


### The actual maximum

... is at $x_\text{max}=1.763$. 



## Why use $d=(\sqrt{5}-1)/2$?

We want to minimize the number of function calls in our search for the function's maximum. Without losing anything meaningful to the logic, we can say our search range is $0\rightarrow L$. To proceed with the Golden Search Method, we choose to investigate two points within the range, located at $x=L_1$ and $x=L_2$. If we think about the symmetry: $L_2+L_1=L$ (and to make sure we are on the same page, the points on the number line in ascending order are: $0$, $L_2$, $L_1$, $L$.)

It would be really neat if we chose the $L_1$ and $L_2$ values such that if we were to refine the range by tossing out, say, $x=L_1\rightarrow L$ from the search, one of the search points in the next iteration would be evaluated already: the one at $L_2$. Our "new range" after the discard would be $0\rightarrow L_1$, and the distance $L_2$ should take up as much of that range as $L_1$ did of the original range $L$. To put it as a ratio:

$$
\frac{L}{L_1}=\frac{L_1}{L_2}.
$$

Now a bit of algebra. Remembering that $L_1+L_2=L$, and defining $R=L_2/L_1$, we can rewrite the above equation as

$$
\frac{L_1+L_2}{L_1}=\frac{L_1}{L_2} \implies 1+\frac{L_2}{L_1}=\frac{L_1}{L_2} \implies 1+R=1/R.
$$

After multiplying-through by $R$ and doing a little rearranging, we arrive at $R+R^2-1=0$, something we can solve via the quadratic equation:

$$
R= \frac{-1\pm \sqrt{5}}{2}.
$$

One of the roots is negative, which doesn't make sense in the context of distances, so we are left with one solution:

$$
d=\frac{\sqrt{5}-1}{2} \approx 0.618.
$$

:::{note}
we usually call $\phi\approx 1.618$ the Golden Ratio. The $d$ we used here is $1/\phi$.
:::
