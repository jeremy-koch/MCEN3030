# Matrix Method for BVPs

Let's describe another option for solving a boundary-value problem (BVP) -- a matrix method. This method can only be applied to linear differential equations ([the Shooting Method](shooting-method.md) works for nonlinear problems, e.g. the [boundary layer equation problem](coupled-eqns.md)). However, it does not require seeds/iterations, and assuming it is well-posed.


## Describe with an example

The video has an example, let's do another one here:

$$
\begin{align*}
& y''-\tfrac{1}{x+1}y'-\cos(x)y = x\\
&\text{ with} ~~ y(0)=1,~~y'(1)=5
\end{align*}
$$

where our goal is to get a numerical description of $y(x)$ between $x=0$ and $1$. (This is a crazy differential equation... I hope you watched the video and saw an easier one first!)

:::{note}
This is still a linear differential equation -- the "output" variable $y$ and it's derivatives appear without powers, are not inside a cosine or anything like that, and do not multiply each other (i.e. no $y y'$).
:::

### Discretize the domain and the derivative(s)

We will discretize the domain with spacing $\Delta x$, and then rewrite the derivatives to be numerical versions with "central differencing". Note that, to avoid bias, we will go from $i-1 \rightarrow i+1$ on the first derivative, and the spacing there is $2\Delta t$. The differential equation becomes:

$$
\left(\frac{y_{i-1}-2y_i + y_{i+1}}{(\Delta x)^2}\right)-\frac{1}{x_i+1}\left(\frac{y_{i+1}-y_{i-1}}{2\Delta x}\right) -\cos(x_i)y_i = x_i
$$

:::{tip}
I would spend some time making sure you understand how this equation was made, and ask me questions about it if you are confused!
:::

### Arriving at the difference equation

Rearrange, grouping into $y_{i-1}$, $y_i$, $y_{i+1}$ terms with coefficients, to arrive at a "difference equation":

$$
\begin{align*}
\left(\frac{1}{(\Delta x)^2}+\frac{1}{2\Delta x (x_i+1)}\right)y_{i-1}
+
\left(\frac{-2}{(\Delta x)^2}-\cos(x_i)\right)&y_{i}\\
+\left(\frac{1}{(\Delta x)^2}-\frac{1}{2\Delta x (x_i+1)}\right)&y_{i+1} = x_i
\end{align*}
$$

To be clear: the "coefficients" are functions of $x$: we can rewrite this equation to be

$$
a(x)y_{i-1}+b(x)y_{i}+c(x) y_{i+1} = f(x)
$$

This is a good strategy when coding! For example, you can define an anonymous function

$$
a(x)=\frac{1}{(\Delta x)^2}+\frac{1}{2\Delta x (x+1)}
$$



Working on it...