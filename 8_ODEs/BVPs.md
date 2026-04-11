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

where our goal is to get a numerical description of $y(x)$ between $x=0$ and $1$. (This is a crazy differential equation... I hope you watched the video to see an easier one first!)

:::{note}
This is still a linear differential equation. The "output" variable $y$ and it's derivatives appear without powers, are not inside a cosine or anything like that, and do not multiply each other (i.e. no $y y'$).
:::

### Discretize the domain and the derivative(s)

We will discretize the domain with spacing $\Delta x$, and then rewrite the derivatives to be numerical versions with "central differencing". Note that, to avoid bias, the first derivative will include $i-1 \rightarrow i+1$, and so the spacing is $2\Delta t$. The differential equation becomes:

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

To be clear: the "coefficients" are functions of $x$. We can rewrite this equation to be something kind of general

$$
a(x_i)y_{i-1}+b(x_i)y_{i}+c(x_i) y_{i+1} = f(x_i).
$$

(We'll see why this is a great idea soon.) What is the meaning of this equation? It is a succinct way of writing a collection of equations

$$
\begin{align*}
a(x_2)y_1 + b(x_2)y_2 + c(x_2)y_3 &= f(x_2)\\
a(x_3)y_2 + b(x_3)y_3 + c(x_3)y_4 &= f(x_3)\\
a(x_4)y_3 + b(x_4)y_4 + c(x_4)y_5 &= f(x_4)\\
a(x_5)y_4 + b(x_5)y_5 + c(x_5)y_6 &= f(x_5)\\
... + ... + ... &= ...
\end{align*}
$$

that is, a system of equations to solve for the temperature values at each node: $i=2\rightarrow N-1$ (where we get to decide how many nodes there are based on the step size $\Delta x$).

### Handling oundary conditions

It is important to understad that we cannot use this difference equation for $i=1$ and $i=N$. Those equations would be

$$
\begin{align*}
a(x_1)y_0 + b(x_1)y_1 + c(x_1)y_2 &= f(x_1) ~??\\
a(x_N)y_{N-1} + b(x_N)y_{N} + c(x_N)y_{N+1} &= f(x_N) ~??
\end{align*}
$$

The problematic terms are $y_0$ and $y_{N+1}$: we only have nodes from $i=1\rightarrow N$, so how can we reference the value of $y$ at the zeroth and $(N+1)\text{th}$ node? So... the differencing scheme only gives us equations for $i=2,3,..., N-1$, yet we have $N$ unknown values of $y_i$. $N-2$ equations, $N$ unknowns?!

We are going to get two more equations by considering the two boundary conditions. The first one is at the first node, i.e. where $x=0$:

$$
y(0)=1 \implies y_1 = 1.
$$

The second (in this problem) is related to the derivative at the node corresponding to $x=L$, i.e. the $N^\text{th}$ node. We again will use a numerical approximation of the derivative, this time a "backwards-differencing" version that just considers the $N$ and $N-1$ nodes:

$$
y'(L) = 5 \implies \frac{y_{N}-y_{N-1}}{\Delta x } = 5 \implies -y_{N-1}+y_{N} = 5\Delta x.
$$

With these two equations, we now have completed the set and have $N$ equations and $N$ unknowns. Framing as a matrix with $N=6$, we can collect the difference equations and boundary equations into

\begin{equation*}
\mathbf{A'}\equiv
\begin{bmatrix}
1 & 0 & 0 & 0 & 0 & 0 \\
a(x_2) & b(x_2) & c(x_2) & 0 & 0 & 0 \\
0 & a(x_3) & b(x_3) & c(x_3) & 0 & 0 \\
0 & 0 & a(x_4) & b(x_4) & c(x_4) & 0 \\
0 & 0 & 0 & a(x_5) & b(x_5) & c(x_5) \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & 0 & -1 & 1
\end{bmatrix}
\begin{bmatrix}
y_1\\ y_2\\ y_3\\ y_4\\ y_5\\ y_6
\end{bmatrix}
=
\begin{bmatrix}
1\\ f(x_2)\\f(x_3)\\f(x_4)\\f(x_5)\\5\Delta x
\end{bmatrix}
\end{equation*}

If we call this system $\mathbf{A}\mathbf{y} = \mathbf{b}$, the solution is $\mathbf{y} =\mathbf{A}^{-1}\mathbf{b}$. We know the value of $x_i$ associated with each value of $y_i$, and so we have a numerical solution to the problem!


## Implementing in your code

Our system is a "tri-diagonal matrix", meaning that, aside from the three longest diagonals, the entries are all zero. We can use this fact, along with our description of $a(x_i)$, $b(x_i)$, $c(x_i)$, and $f(x_i)$, to build up a matrix with relatively few commands. 

### Using $a(x_i)$, etc.

We can implement $a(x_i)$, $b(x_i)$, $c(x_i)$, and $f(x_i)$ anonymous functions in our code, and then call those functions using a vector of $x_i$ values. We then will have one-dimensional arrays for the $a$, $b$, and $c$ diagonals, and the forcing function $f$, at least for the interior points.

:::{caution}
We only want to use the interior points, $x_2\rightarrow x_{N-1}$. So create your $a$ values by inputting just ```x(2:N-1)```.
:::

### Creating a diagonal matrix

We will use these one-dimensional arrays to create the tri-diagonal matrix via a built-in matrix construction command. These commands are mentioned in the [coding elements overview pages](./1_prog-basics/coding-elements-overview.md) but I'll repeat them here and put them into context.

After creating arrays ```a_vals``` (for values of $a(x_i)$), etc., the construction of the matrix can be done in one line. Note that the boundary conditions are being included!

::::{tab-set}
:::{tab-item} MATLAB
```matlab
A=diag([1,b_vals, 1],0)+diag([a_vals, -1],-1)+diag([0,c_vals],1);
```
:::


:::{tab-item} Python
```python
A = np.diag(np.r_[1, b_vals, 1], 0) + np.diag(np.r_[a_vals, -1], -1) + np.diag(np.r_[0, c_vals], 1)
```
:::


:::{tab-item} Julia
```julia
using LinearAlgebra

A = Tridiagonal([a_vals; -1], [1; b_vals; 1], [0; c_vals])
```
:::
::::

Then just create the forcing function from ```f_vals``` and the boundary condition information, and you are pretty much done!