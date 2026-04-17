# The Heat Equation (a PDE)

In this class we will focus our attention on [parabolic PDEs](https://en.wikipedia.org/wiki/Parabolic_partial_differential_equation), and [the Heat Equation](https://en.wikipedia.org/wiki/Heat_equation) is the canonical example of that class of equations.

:::{seealso}
If you are interested: [Laplace's Equation](https://en.wikipedia.org/wiki/Laplace%27s_equation) is an example of an [elliptic PDE](https://en.wikipedia.org/wiki/Elliptic_partial_differential_equation), and [the Wave Equation](https://en.wikipedia.org/wiki/Wave_equation) is an example of a [hyperbolic PDE](https://en.wikipedia.org/wiki/Hyperbolic_partial_differential_equation).
:::

The mathematical problem is:

$$
\frac{\partial u}{\partial t} = \alpha \frac{\partial^2 u}{\partial x^2}
$$

on a domain $x:x_\text{L}\rightarrow x_\text{R}$ with known boundary conditions at $u(t,x_L)$ and $u(t,x_R), and a known initial condition $u(0,x)$.

## Discretizing the problem