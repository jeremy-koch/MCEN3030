# Taylor Series Refresher


**Author:** Jeremy Koch

## The Taylor Series

Suppose we have a complicated function $f(x)$, made of natural logs and arctangents or whatever. Not friendly to deal with. We could reasonably ask the question: if there is another function $\hat{f}(x)$ that has the same value as $f(x)$ at $x=x_0$, and the same value of the first derivative (so the value of $\hat{f}(x)$ is changing just as rapidly as $f(x)$ at $x=x_0$), and the same value of the second derivative (so the rate of change of the rate of change of $\hat{f}(x)$ matches that of $f(x)$), and the same value of the third derivative, and the same value of the fourth derivative, etc., onwards to the infinitieth derivative... well, that sounds like we effectively have the same functional behavior for both $f(x)$ and $\hat{f}(x)$. A function that meets this requirement can usually be constructed:
\begin{equation}
\hat{f}(x) = f(x_0)+ f'(x_0)(x-x_0) + \frac{1}{2!}f''(x_0)(x-x_0)^2 + \dots + \frac{1}{N!}f^{(N)}(x_0)(x-x_0)^N.
\end{equation}
:::{aside}
At $x=x_0$, all terms but the first becomes zero, and so the above function matches the value $f(x_0)$. Take the first derivative and evaluate at $x=x_0$: again, most of the terms becomes zero, and we are left with $\hat{f}'(x_0)=f'(x_0)$. On and on for all derivatives.
:::
Importantly, this equivalent function, $\hat{f}(x)$, is a polynomial, and polynomials are easy to deal with! The trade-off, of course, is that there are now infinity terms. We'll see if we can tame that.

## Error

We could characterize the error between the original function $f(x)$ and the equivalent polynomial $\hat{f}(x)$ at an arbitrary point $x$ via
\begin{equation}
\text{error} = f(x) - \hat{f}(x) = f(x) - \left[f(x_0)+ f'(x_0)(x-x_0) + \frac{1}{2!}f''(x_0)(x-x_0)^2 + \dots \right]
\end{equation}


## Linearization

Let's suppose $x-x_0=\epsilon$, where $\epsilon \ll 1$. To make it concrete, let's say $\epsilon=0.1$. What is the value, then, of $(x-x_0)^2 = \epsilon^2$? It is small: 0.01. And $(x-x_0)^3 = \epsilon^3$? Even smaller, 0.001. This tells us that, presuming the function 

The most important lesson we learn from Taylor Series is how to approximate a function as a line, at least "near" to a point. Notice that in the "full" Taylor Series $x+4$


