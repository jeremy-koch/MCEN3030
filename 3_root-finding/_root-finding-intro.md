# Root-Finding Methods Intro


Most of your work in traditional lecture classes involves pushing around equations until you can settle on something like:
\begin{equation}
    F = \frac{\pi}{2}\rho U^2 R^2.
\end{equation}
That is, you can usually "explicitly" solve for the variable you are interested using algebra. In practice, it doesn't always work out so neatly. A classic example is the Colebrook Equation, which is used to determine the pressure drop in pipe flow:
\begin{equation}
    \frac{1}{\sqrt{f}} = -2 \log\left(\frac{\epsilon/D}{3.7}+\frac{2.51}{\text{Re}\sqrt{f}}\right)
\end{equation}
Notice that $f$ appears both within the logarithm argument and outside the logarithm argument. This means it can't be solved for explicitly... i.e., you cannot arrive at $f=\text{something}$ where the "something" is fundamental mathematical functions like $\exp$, $\log$, etc. To solve these problems, engineers have traditionally looked at a chart -- [the Moody Diagram](https://en.wikipedia.org/wiki/Moody_chart). But we can also use "root-finding methods" to solve algebraic equations.


## Root-Finding Algorithms

This type of problem could be called "algebraic equation solving", but actually we need to use the special properties of zero in our algorithms. That is, we must examine an equation in the form $g(x)=0$, and we are finding the roots: the $x$-locations that make $g(x)=0$.
:::{aside}
Any equation, $A(x)=B(x)$ can be turned into a root-finding problem by rearranging to $A(x)-B(x)=0$ and then working with $g(x)\equiv A(x)-B(x)$. For example, with the Colebrook Equation, we might manipulate it to
\begin{equation}
    \frac{1}{\sqrt{f}} +2 \log\left(\frac{\epsilon/D}{3.7}+\frac{2.51}{\text{Re}\sqrt{f}}\right) =0
\end{equation}
:::

## Types of Root-Finding Methods

There are two classes of root-finding methods: 

"Bracketed" methods are called as such because you place a lower and upper limit on your search range. These have a few downsides in general:
- You must have some idea of where the root is located.
- They tend to be slow to converge.
- If there are two roots within the range, the algorithm may break.
However, at least if there is only one root within the brackets, it is guaranteed to find it.


"Open" methods are called as such because their search range is not limited. The downsides are:
- They are not guaranteed to find the root. 
- Because they aren't confined to a certain region, they may accidentally find "the wrong root". E.g. you want the positive solution, you find the negative one.
- You may need to do some prep work, e.g. calculating a derivative or rearranging $g(x)=0$ to something slightly different, a $h(x)=0$ (e.g., $h(x)\equiv g(x)/x$... it is still equal to zero).
However, they can converge more quickly than bracketed methods. Additionally, the main one we will discuss (Newton-Raphson) can be implemented in higher dimensions -- it works for $g(x)=0$; it also works for the system $f(x,y)=0$, $g(x,y)=0$; and further, with $f(x,y,z)=0,g(x,y,z)=0,h(x,y,z)=0$.
:::{aside}
Even higher dimensions too, but I don't want to write it out!
:::

## The wrong way to do it

The following will get you the root if one exists on a given range. Let's assume we have a lower limit to the search, ```x_L```, and upper limit to the search, ```x_U```, and a spacing ```dx```. And we'll just use an anonymous function defined as ```f```.
::::{tab-set}
:::{tab-item} MATLAB
```matlab
x=x_L:dx:x_U;
y=f(x);
[~,idx]=min(abs(y));
x_root=x(idx);
```
:::
:::{tab-item} Python
```python
x = np.arange(x_L, x_U, dx)
y = f(x)
idx = np.argmin(np.abs(y))
x_root = x[idx]
```
:::
:::{tab-item} Julia
```
x = x_L:dx:x_U
y = f.(x)
_, idx = findmin(abs.(y))
x_root = x[idx]
```
:::
::::
The downside of this approach is: we calculated the value of the function at every value of $x$, and then performed a second operation that checked over all of those values (```min```/```argmin```/```findmin```). A lot of calculations! We will call this a "brute force" method, because we are essentially just checking every possibility.

We will see that the methods described in this unit can achieve the same goal with significantly fewer operations, meaning they are much faster.

:::{tip}
We will write functions for these algorithms, and the equation $f(x)$ will be an input to those functions. Revisit [anonymous functions in the coding elements pages](../1_prog-basics/coding-elements-overview.md)... that is how we will do it!
:::