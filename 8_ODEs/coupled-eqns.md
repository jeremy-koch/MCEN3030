# Coupled and Higher-Order Equations




### Quick aside on mathematical chaos





## Higher-Order Equations

Any higher-order differential equation can be reduced to a set of coupled first-order differential equations. Let's do two quick examples.

### Example 1

This is a nonlinear differential equation with a known forcing function $G(t)$. Write the equation such that the highest derivative is by itself

$$
\frac{d^2 x}{dt^2} = \mu (1-x^2)\frac{dx}{dt}- x - G(t)
$$

and then define a new variable, $u(t) = dx/dt$. We then have two first-order equations:

$$
\begin{align}
\frac{dx}{dt} &= u\\
\frac{du}{dt} &= \mu (1-x^2)u- x - G(t)
\end{align}
$$

:::{hint}
The left-hand side of these equations are just a single first-order derivative. There are no derivatives on the right-hand side of these equations: where we saw $dx/dt$, we replaced it with $u$.
:::

Because the original equation was second order, we needed two initial conditions: $x(0)=x_0$ and $x'(0)=u_0$. 

### Example 2

This equation comes up in boundary layer theory. We won't be able to solve it until we learn the Shooting Method, but we can set it up. I'll use primes $'$ to denote derivatives.

$$
f''' = -\tfrac{1}{2} f\cdot f''
$$

Now we will need to define two new variables: $g=f'$ and $h=g'=f''$. We then arrive at a system with three equations:

$$
\begin{align}
f' &= g\\
g' &= h\\
h' &= -\tfrac{1}{2} f\cdot h
\end{align}
$$

:::{note} Note again
Single derivatives on the left-hand side, no derivatives on the right-hand side.
:::

## Implementing in your program

We wish to write a generic program that can take in coupled equations and produce the numerical solution. Here is how we might do it:

::::{tab-set}
:::{tab-item} MATLAB
```matlab

[x,t]=RK4(f)
```
:::
:::{tab-item} Python
```python

???
```
:::
:::{tab-item} Julia
```julia

???
```
:::

::::