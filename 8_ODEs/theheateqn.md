# The Heat Equation (a PDE)

In this class we will focus our attention on [parabolic PDEs](https://en.wikipedia.org/wiki/Parabolic_partial_differential_equation), and [the Heat Equation](https://en.wikipedia.org/wiki/Heat_equation) is the canonical example of that class of equations.

:::{seealso}
If you are interested: [Laplace's Equation](https://en.wikipedia.org/wiki/Laplace%27s_equation) is an example of an [elliptic PDE](https://en.wikipedia.org/wiki/Elliptic_partial_differential_equation), and [the Wave Equation](https://en.wikipedia.org/wiki/Wave_equation) is an example of a [hyperbolic PDE](https://en.wikipedia.org/wiki/Hyperbolic_partial_differential_equation).
:::

The mathematical problem is:

$$
\frac{\partial T}{\partial t} = \alpha \frac{\partial^2 T}{\partial x^2}
$$

on a domain $x:x_\text{L}\rightarrow x_\text{R}$ with known boundary conditions at $u(t,x_L)$ and $u(t,x_R)$, and a known initial condition $u(0,x)$.

## Discretizing the problem

As we did with [BVPs](BVPs.md), we will discretize the derivatives. The thing we have to be careful of is the fact that we need two indices to keep track of where we are in time and space. We'll use $i$ as our time index and $j$ as our space index. Then the heat equation is discretized to

$$
\frac{u_{i+1,j}-u_{i,j}}{\Delta t} = \alpha \frac{u_{i,j+1}-2u_{i,j}+u_{i,j-1}}{(\Delta x)^2}
$$

where $\Delta t$ and $\Delta x$ are the (chosen) time and position spacing. Then, after a small rearrangement:

$$
u_{i+1,j}= u_{i,j} +\frac{\alpha \Delta t}{(\Delta x)^2} \left(u_{i,j+1}-2u_{i,j}+u_{i,j-1}\right).
$$

:::{caution}
There are limitations on the allowable values of $\alpha \Delta t/(\Delta x)^2$ if we want a stable solution (which we do!). See below.
:::

This equation should be reminiscent of [RK4](runge-kutta.md): we use information at our current time step, $i$, to figure out information at our next time step, $i+1$. We just have the added complication that we are not just referencing the $j$ node's value at $i$, we have to consider the neighbors' values as well: the value of $u_{i+1,j}$ depends on $u_{i,j}$ and $u_{i,j-1}$ and $u_{i,j+1}$.

## Marching forward from the initial condition (the algorithm)

Remember that we have supplied an initial condition. We use this to get the values of $u_{1,j}$ for all $j$.

Then we find the values of $u_{2,j}$ for $j=2$ to $N-1$ (assuming there are $N$ spatial nodes) using the update equation from above. This could be done with ```for``` loop... inside the time-marching ```for``` loop.

Before we finish that time step, we need to set the boundary values. Generically, we could write the boundary condition as

$$
a_0(t) u(t,0) + b_0(t) u'(t,0) = c_0(t)
$$

(assuming the boundary is at $x=0$, and $u'$ is the derivative with respect to $x$). Discretizing:

$$
a_0(t)u_{i+1,1} + b_0(t)\frac{u_{i+1,2}-u_{i+1,1}}{\Delta x} = c_0(t)
$$

and, recognizing that at this point in the algorithm $u_{i+1,2}$ is known:

$$
u_{i+1,1}=\left[\frac{1}{a_0(t)-b_0(t)/\Delta x}\right]\left[c_0(t)-\frac{b_0(t)}{\Delta x}u_{i+1,2}\right]
$$

gives us the unknown value at the left boundary.

On the other boundary (say at $x=L$) we will have something similar:

$$
a_L(t) u(t,L) + b_L(t) u'(t,L) = c_L(t)
$$

leading to 

$$
a_L(t)u_{i+1,N} + b_L(t)\frac{u_{i+1,N}-u_{i+1,N-1}}{\Delta x} = c_L(t)
$$

leading to

$$
u_{i+1,N}=\left[\frac{1}{a_L(t)-b_L(t)/\Delta x}\right]\left[c_L(t)+\frac{b_L(t)}{\Delta x}u_{i+1,N-1}\right].
$$



### Dirichlet boundary condition

Implementing the generic boundary conditions looks complicated... actually it isn't too bad, particularly because we will focus on non-time varying boundary conditions.

FYI, the boundary condition $u(t,0)=u_0$ would simply have: $a_0(t)=1$, $b_0(t)=0$, $c_0(t)=u_0$. Thus:

$$
u_{i+1,1}=u_0.
$$

### Neumann boundary condition

the boundary condition $u'(t,0)=W$ would simply have: $a_0(t)=0$, $b_0(t)=1$, $c_0(t)=W$. Thus:

$$
u_{i+1,1}=u_{i+1,2}.
$$



## Stability

Added soon.