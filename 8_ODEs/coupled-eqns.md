# Coupled and Higher-Order Equations

The time-stepping process can be applied to coupled equations of the form

$$
\begin{align}
\frac{dx}{dt} &= f(t,x,y,z)\\
\frac{dy}{dt} &= g(t,x,y,z)\\
\frac{dz}{dt} &= h(t,x,y,z)
\end{align}
$$

(with initial conditions $x_0,y_0,z_0$). In our calculation of $x_{i+1}$ we will need to evaluate $f(t_i,x_i,y_i,z_i)$, and similar for $y$ and $z$. No problem! 

## $k_{1x}$, etc.

$$
\begin{align}
x_{i+1}&=x_i + \Delta t\left(\frac{k_{1x} + 2k_{2x} + 2k_{3x} + k_{4x}}{6} \right)\\
y_{i+1}&=y_i + \Delta t\left(\frac{k_{1y} + 2k_{2y} + 2k_{3y} + k_{4y}}{6} \right)\\
z_{i+1}&=z_i + \Delta t\left(\frac{k_{1z} + 2k_{2z} + 2k_{3z} + k_{4z}}{6} \right)
\end{align}
$$

where

$$
\begin{align}
k_{1x} &= f(t_i , x_i , y_i , z_i )\\
k_{1y} &= g(t_i , x_i , y_i , z_i )\\
k_{1z} &= h(t_i , x_i , y_i , z_i )
\end{align}
$$

and

$$
\begin{align}
k_{2x} &= f(t_i+\tfrac{1}{2}\Delta t , x_i+\tfrac{1}{2}\Delta t\cdot k_{1x}, y_i+\tfrac{1}{2}\Delta t\cdot k_{1y}, z_i+\tfrac{1}{2}\Delta t\cdot k_{1z} )\\
k_{2y} &= g(t_i+\tfrac{1}{2}\Delta t , x_i+\tfrac{1}{2}\Delta t\cdot k_{1x}, y_i+\tfrac{1}{2}\Delta t\cdot k_{1y}, z_i+\tfrac{1}{2}\Delta t\cdot k_{1z} )\\
k_{2z} &= h(t_i+\tfrac{1}{2}\Delta t , x_i+\tfrac{1}{2}\Delta t\cdot k_{1x}, y_i+\tfrac{1}{2}\Delta t\cdot k_{1y}, z_i+\tfrac{1}{2}\Delta t\cdot k_{1z} )
\end{align}
$$

and

$$
\begin{align}
k_{3x} &= f(t_i+\tfrac{1}{2}\Delta t , x_i+\tfrac{1}{2}\Delta t\cdot k_{2x} , y_i+\tfrac{1}{2}\Delta t\cdot k_{2y} , z_i+\tfrac{1}{2}\Delta t\cdot k_{2z})\\
k_{3y} &= g(t_i+\tfrac{1}{2}\Delta t , x_i+\tfrac{1}{2}\Delta t\cdot k_{2x} , y_i+\tfrac{1}{2}\Delta t\cdot k_{2y} , z_i+\tfrac{1}{2}\Delta t\cdot k_{2z})\\
k_{3z} &= h(t_i+\tfrac{1}{2}\Delta t , x_i+\tfrac{1}{2}\Delta t\cdot k_{2x} , y_i+\tfrac{1}{2}\Delta t\cdot k_{2y} , z_i+\tfrac{1}{2}\Delta t\cdot k_{2z})
\end{align}
$$

and

$$
\begin{align}
k_{4x} &= f( t_i+\Delta t , x_i+\Delta t\cdot k_{3x} , y_i+\Delta t\cdot k_{3y} , z_i+\Delta t\cdot k_{3z})\\
k_{4y} &= g( t_i+\Delta t , x_i+\Delta t\cdot k_{3x} , y_i+\Delta t\cdot k_{3y} , z_i+\Delta t\cdot k_{3z})\\
k_{4z} &= h( t_i+\Delta t , x_i+\Delta t\cdot k_{3x} , y_i+\Delta t\cdot k_{3y} , z_i+\Delta t\cdot k_{3z}).
\end{align}
$$

Seems like a lot, but we are going to handle these as arrays, and so the [code we write](RK4-starter.md) will actually be quite succinct!


### Mathematical chaos

You may be interested to read about [the Lorenz System](https://en.wikipedia.org/wiki/Lorenz_system) whose analysis ignited the field of [mathematical chaos](https://en.wikipedia.org/wiki/Chaos_theory). These nonlinear equations are not solveable analytically but are easily handled numerically (and are indeed a classic example of RK4 applied to coupled equations).


## Higher-Order Equations

Any higher-order differential equation can be reduced to a set of coupled first-order differential equations. Let's do two quick examples.

### Example 1

A nonlinear differential equation with a known forcing function $G(t)$, where we've written the equation such that the highest derivative is by itself on the left-hand side:

$$
\frac{d^2 x}{dt^2} = \mu (1-x^2)\frac{dx}{dt}- x - G(t).
$$

Define a new variable, $u(t) = dx/dt$, and we then have two first-order equations:

$$
\begin{align}
\frac{dx}{dt} &= u\\
\frac{du}{dt} &= \mu (1-x^2)u- x - G(t).
\end{align}
$$

Because the original equation was second order, we needed two initial conditions: $x(0)=x_0$ and $x'(0)=u_0$. Now those become the initial conditions of the two first-order equations: $x(0)=x_0$ and $u(0)=u_0$.

:::{hint}
The left-hand side of both of these equations is just a single first-order derivative. There are no derivatives on the right-hand side of these equations. Where we saw $dx/dt$, we replaced it with $u$.
:::



### Example 2

This equation comes up in boundary layer theory. One of the boundary conditions is at infinity, so we won't be able to solve it until we learn the Shooting Method, but we can set it up. I'll use primes $'$ to denote derivatives.

$$
x''' = -\tfrac{1}{2} x\cdot x''
$$

We will need to define two new variables: $y=x'$ and $z=y'=x''$. We then arrive at a system with three equations:

$$
\begin{align}
x' &= y\\
y' &= z\\
z' &= -\tfrac{1}{2} x\cdot z
\end{align}
$$

:::{hint} Note again
Single derivatives on the left-hand sides, no derivatives on the right-hand sides.
:::

## Implementing in your program

See [RK4 starter](RK4-starter.md).