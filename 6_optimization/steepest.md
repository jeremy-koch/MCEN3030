# Steepest Ascent

The Method of Steepest Ascent is a method for optimizing higher-dimensional functions such as $f(x,y)$ or $f(x_1,x_2,x_3,...)$.

The idea is this: if we would like to improve upon an initial guess for the location of the function maximum, where should we look? You may recall from Calculus 3 that the [gradient](https://en.wikipedia.org/wiki/Gradient)

$$
\nabla f = \left<\frac{\partial f}{\partial x_1},\frac{\partial f}{\partial x_2},\frac{\partial f}{\partial x_3},...\right>
$$

points in the direction that will most rapidly increase the function. It makes sense, then, to look in the direction of the gradient.

Almost all of the algorithms we teach in this class are about achieving some goal systematically and with the least computational effort possible. We could take an incremental step in that direction, recalculate the gradient at the new point, take another incremental step in that direction, recalculate the gradient, ... . That is a strategy used in some applications, but we are going to do something that will converge more quickly: we are going to do a one dimensional search through a new variable $s$ that is something like a distance from our previous best guess for the maximum.
:::{warning}
$s$ is proportional to the distance from the previous guess, but it is not the actual distance.
:::
Once we find the max along that path, that is our new best guess for the maximum of $f(x_1,x_2,...)$, and we recalculate the gradient at that point and then perform a new search along that new path.

We will use [the Golden Search Method](golden.md) as our one-variable search algorithm.

:::{seealso}
You may hear about [Gradient Descent](https://en.wikipedia.org/wiki/Gradient_descent) in machine learning. It's basically the same idea, but we are moving opposite to the gradient direction... "steepest descent".
:::

## Using $s$ as our one variable

The gradient has a magnitude and direction. A couple of observations:
- If we multiply the gradient by a scalar $s$, we change its magnitude but not it's direction.
- The angle that we move from our initial location depends on the ratio of the components of the derivatives. I.e.:

$$
\theta = \arctan\left(\frac{\partial f/\partial y}{\partial f/\partial x}\right)
$$

From these truths, we can rewrite our $x$- and $y$-coordinates like this:

$$
x  = x_i +\frac{\partial f}{\partial x}\bigg\rvert_i \cdot s\\
y = y_i +\frac{\partial f}{\partial y}\bigg\rvert_i \cdot s
$$

and we know that $(x,y)$ will be along the gradient line calculated at $(x_i,y_i)$.
:::{caution}
If $(x_0,y_0)=(0,0)$ with $\partial f/\partial x=100$ and $\partial f/\partial y=0$ at $(0,0)$, we have $x=100s$ and $y=0$. This should convince you that $s$ is not just the distance from the previous iteration: a step of $1$ in $s$ causes us to move $100$ in $x$!
:::
:::{note} Think
If we have a function of eight variables, $f(x_1, x_2, ... x_8)$, how would we relate $s$ to $x_1,x_2,...$?
:::

### A quick example

Suppose $f(x,y)=\exp(-x^2-y^2)$ and we are trying to use Steepest Ascent, beginning at $(x_0,y_0)=(0.2,0.3)$. The gradient is

$$
\nabla f =\left<-2x\exp(-x^2-y^2),-2y\exp(-x^2-y^2)\right>.
$$

Evaluated at the seed, the gradient is $<-0.35,-0.53>$. Then using this along with our definition relating $x$ and $y$ to $s$ to write

$$
x=0.2 -0.35 s\\
y=0.3 -0.53 s.
$$

We then can rewrite $f(x,y)$ as

$$
f(s)=\exp[-(0.2-0.35s)^2-(0.3-0.53s)^2].
$$

We can then plug this function of one variable in to our [Golden Search](golden.md) code to find the maximum in the direction of the gradient.


## Algorithm

0\. This is an iterative method, so we will again start with a seed as our "best guess".  
1\. Evaluate the gradient at the current best guess and use the above equations to relate $x$ and $y$ to $s$ (via $(x_i,y_i)$ and the gradient components). We can then rewrite $f(x,y)$ as $f(s)$.  
2\. Use the Golden Search Method to determine the maximum in the gradient direction. (See below for a discussion on the bounds.)  
3\. When the max is located, in terms of $s$, again use the equations relating $x$ and $y$ to $s$ to determine our new "best guess".  
4\. Iterate until acceptably converged.


### Choosing the bounds of the Golden Search

There are a few options. The first two will have you setting the lower bound of the search as $s=0$.

1. If there is a particular domain you are searching, e.g. $x_L < x < x_U$ and $y_L < y < y_U$, you can use the relationship between $s$ and $x$ and $s$ and $y$ to determine how far you can displace in $s$ before reaching one of those limits.
2. You can just choose a constant maximum size $s_\text{step}$. If the size is too small, no problem: you will identify that the max occurs at $s_\text{step}$ and then will just do another iteration more-or-less in the same gradient direction. The downside of this is that it will take more iterations.
3. A modification to (2): you can test the waters with $s=s_\text{step}$ and $s=2s_\text{step}$.  
- If $f(s_\text{step})<f(2s_\text{step})$, examine $f(3s_\text{step})$. 
- If $f(2s_\text{step})<f(3s_\text{step})$, examine $f(4s_\text{step})$.
- ...
- Eventually you will get to a case where $f(ks_\text{step})>f((k+1)s_\text{step})$. You can then perform the Golden Search from $s=ks_\text{step}$ to $s=(k+1)s_\text{step}$.




### Convergence

As we find our way towards the maximum, the distance between consecutive "best guesses" will get smaller and smaller.


### Numerical vs. Analytical Gradient

It is possible to use either analytical expressions for the gradient, e.g. implemented as a series of anonymous functions, or a numerical version, as we did with [non-linear fitting](../5_fitting/nonlinear.md).

Reminder how the numerical version would work: we'd pick a small step $h$ (maybe $10^{-8}$) to approximate the derivative:

$$
\frac{\partial f}{\partial x_i} = \approx \frac{f(...,x_i+h, ...)-f(...,x_i, ...)}{h}.
$$

We'd need to "perturb" each of the inputs by $h$, but then would have an estimate for the gradient and can proceed with the algorithm.