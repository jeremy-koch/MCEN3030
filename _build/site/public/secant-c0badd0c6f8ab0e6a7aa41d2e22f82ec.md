# The Secant Method

Briefly: There is a cousin to Newton-Raphson Method known as "The Secant Method", which notably does not require us to calculate and input an analytical derivative into the algorithm.

## The algorithm

The algorithm is very similar to [Newton-Raphson](1D-NR.md), whose equation I will repeat here:
$$
x_i=x_{i-1}- \frac{f(x_{i-1})}{f'(x_{i-1})}.
$$
Instead of an analytical derivative, we compute an approximate derivative:
$$
f'(x_{i-1})\approx \frac{f(x_{i-1})-f(x_{i-2})}{x_{i-1}-x_{i-2}}
$$
so that the algorithm's core equation becomes
$$
x_i=x_{i-1}- f(x_{i-1})\frac{x_{i-1}-x_{i-2}}{f(x_{i-1})-f(x_{i-2})}.
$$
We will need two seed guesses to get this started, but otherwise the algorithm matches that of Newton-Raphson.

## Picking the seed guesses

As with all open methods, there is a chance that this algorithm does not converge, and so seed choice can be important. However, while spiritually we are approximating the analytical derivative, the algorithm does not need us to choose an infinitesimal separation between seed values.

A demo: In this first case, the seed values are 0.5 and 0.6, and so the secant line is similar to the tangent line.
```{figure} secant_1.png
:alt: 
:width: 100%
:align: center

Secant Method with seeds 0.5 and 0.6, for $f(x) = exp(x)-3.91$. The initial secant line is reminiscent of the tangent line at $x=0.6$, but that is not the case with further iterations. Yet we still converge!
```

Same problem, but now the seed values are 0 and 1.9.
```{figure} secant_2.png
:alt: 
:width: 100%
:align: center

Secant Method with seeds 0 and 1.9, again for $f(x) = exp(x)-3.91$. The initial secant line is not at all reminiscent of the tangent line at $x=0$ or $x=1.9$, yet we still converge to the root.
```

:::{tip}
Trace these paths and make sure you understand how the points are related by this algorithm.
:::