# Newton-Raphson Method (2+D)

The [(1D) Newton-Raphson Method](1D-NR.md) can be extended to higher dimensional systems. Suppose we have two equations,
$y=mx+b$ and $x^2 + y^2 = R^2$, with known constants $m$, $b$, and $R$.
:::{note}
So, a line and a circle. Keep in mind that there may be zero, one, or two solutions...
:::

We can rearrange this into the system:
$$
mx-y+b=0\\
x^2+y^2-R^2=0
$$
and call that first equation $f(x,y)=0$ and the second $g(x,y)=0$. So it is like a simultaneous root-finding problem. The [Taylor Series idea](../2_foundations/Taylor-Series.md) can be extrapolated to 2+ dimensions based on a reference location $(x_0,y_0)$. Examining the linearized versions of general $f$ and $g$:
$$
f(x,y)\approx f(x_0,y_0) + \frac{\partial f}{\partial x}\bigg\rvert_0 (x-x_0) + \frac{\partial f}{\partial y}\bigg\rvert_0 (y-y_0)\\
g(x,y)\approx g(x_0,y_0) + \frac{\partial g}{\partial x}\bigg\rvert_0 (x-x_0) + \frac{\partial g}{\partial y}\bigg\rvert_0 (y-y_0)
$$
where, e.g., $\partial f/\partial y\rvert_0$ is evaluated at $(x_0,y_0)$. Similar to in the 1D case, we can set $f(x,y)=0$ and $g(x,y)=0$ and rearrange to:
$$
\frac{\partial f}{\partial x}\bigg\rvert_0 (x-x_0) + \frac{\partial f}{\partial y}\bigg\rvert_0 (y-y_0) = -f(x_0,y_0)\\
\frac{\partial g}{\partial x}\bigg\rvert_0 (x-x_0) + \frac{\partial g}{\partial y}\bigg\rvert_0 (y-y_0)= -g(x_0,y_0)
$$
and can then reframe this as a matrix system, defining $\Delta x\equiv x-x_0$ and $\Delta y=y-y_0$:
\begin{equation}
\begin{bmatrix}
\frac{\partial f}{\partial x} & \frac{\partial f}{\partial y}\\
\frac{\partial g}{\partial x} & \frac{\partial g}{\partial y}
\end{bmatrix}_0
\begin{bmatrix}
\Delta x\\ \Delta y
\end{bmatrix}
=
\begin{bmatrix}
-f\\ -g
\end{bmatrix}_0.
\end{equation}
Note that the matrix and right-hand side of this equation are evaluated at the reference location to determine the unknown vector of displacements $(\Delta x,\Delta y)$.
:::{note}
A matrix full of partial derivatives like this is called "The Jacobian". And in the general linear algebra problem $\mathbf{Ax}=\mathbf{b}$, the $\mathbf{b}$ is sometimes called "the forcing function" -- in this context, the further $f$ and $g$ are from zero, the greater $\Delta x$ and $\Delta y$ are, and so there is a greater "push" from the current location.
:::

As was the case with the 1D Newton-Raphson Method, we think about this not as a single step, but rather an iterative scheme:
\begin{equation}
\begin{bmatrix}
\frac{\partial f}{\partial x} & \frac{\partial f}{\partial y}\\
\frac{\partial g}{\partial x} & \frac{\partial g}{\partial y}
\end{bmatrix}_i
\begin{bmatrix}
\Delta x\\ \Delta y
\end{bmatrix}_i
=
\begin{bmatrix}
-f\\ -g
\end{bmatrix}_i
\end{equation}
where $x_{i+1}=x_i + \Delta x_i$ and $y_{i+1} = y_i +\Delta y_i$.

## The algorithm

The algorithm matches that of the 1D Newton-Raphson method, but let's clarify the details.

1. The two functions and four partial derivatives must be provided as functions, as well as a seed value.
2. The Jacobian and forcing function of the iterative equation above can be evaluated.
3. Solving the matrix system tells us how to update our estimation of the solution.
4. Iterate until convergence or until we give up.

## Solving the matrix system

Finding the inverse of a matrix is actually a challenging computational problem. We will learn a computer-friendly version of Gaussian Elimination shortly, but for a small system like this, [Cramer's Rule](../2_foundations/Cramer.md) is reasonable.