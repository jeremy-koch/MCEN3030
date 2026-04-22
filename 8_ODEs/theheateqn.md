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

The boundary condition $u'(t,0)=W$ would simply have: $a_0(t)=0$, $b_0(t)=1$, $c_0(t)=W$. Thus:

$$
u_{i+1,1}=-W\Delta x+u_{i+1,2}.
$$

And a special case: the "adiabatic boundary" condition, $W=0$:

$$
u_{i+1,1}=u_{i+1,2}.
$$


## Stability

:::{caution}
If

$$
\frac{\alpha \Delta t}{(\Delta x)^2}>\frac{1}{2}
$$

the algorithm is unstable. 
:::

We should have reason to be suspicious of our numerical solution when $\alpha \Delta t/(\Delta x)^2$ is large. Revisiting our time-stepping equation:

$$
u_{i+1,j}= u_{i,j} +\frac{\alpha \Delta t}{(\Delta x)^2} \left(u_{i,j+1}-2u_{i,j}+u_{i,j-1}\right).
$$

we see that node $j$ is influenced by nodes $j-1$, $j$, and $j+1$. That is, heat is being exchanged between these nodes, and we are attempting to keep track of that by creating a numerical solution for $T$. But if $\alpha \Delta t/(\Delta x)^2$ is large, it means heat is diffusing too quickly and/or we are "paying attention" too infrequently (large $\Delta t$) to properly account for it. Physically node $j$ would be receiving heat from $j\pm 2$, $j\pm 3$, etc., within the timestep $\Delta t$.

How does this look numerically? Let's consider a system with 5 nodes and with $\alpha \Delta t/(\Delta x)^2=0.4$. We'll take a linear initial condition, $T_{1,j}=[0,1,2,3,4]$ and boundary conditions $T(t,0)=0=T(t,L)$. for $t>0$, there will be a very sharp peak in the temperature profile at $x=L$, owing to the immediate application of the boundary condition. That sharp peak SHOULD soften with time, and physically we expect that process to be smooth and gradual. Indeed, here are the first few time steps:
```
0    1.0000    2.0000    3.0000    4.0000
0    1.0000    2.0000    3.0000         0
0    1.0000    2.0000    1.4000         0
0    1.0000    1.3600    1.0800         0
0    0.7440    1.1040    0.7600         0
0    0.5904    0.8224    0.5936         0
0    0.4470    0.6381    0.4477         0
0    0.3446    0.4855    0.3448         0
0    0.2631    0.3729    0.2632         0
0    0.2018    0.2851    0.2018         0
```
The solution will soon "settle down" to ```0 0 0 0 0```, which is what we expect physically. That is good news for the trustworthiness of our analysis.



If, instead, we set the problem up such that $\alpha \Delta t/(\Delta x)^2=0.6$, here are the first few time steps:
```
0    1.0000    2.0000    3.0000    4.0000
0    1.0000    2.0000    3.0000         0
0    1.0000    2.0000    0.6000         0
0    1.0000    0.5600    1.0800         0
0    0.1360    1.1360    0.1200         0
0    0.6544   -0.0736    0.6576         0
0   -0.1750    0.8019   -0.1757         0
0    0.5162   -0.3708    0.5163         0
0   -0.3257    0.6936   -0.3257         0
0    0.4813   -0.5296    0.4813         0
```
Whoa, negative values? That doesn't make sense physically...

:::{warning}
Always obey the Second Law of Thermodynamics.
:::

And, actually, if we examine at later times.
```
A FEW MOMENTS LATER
0   15.6833  -22.1795   15.6833         0
0  -16.4444   23.2558  -16.4444         0
0   17.2424  -24.3844   17.2424         0
0  -18.0791   25.5677  -18.0791         0
0   18.9565  -26.8085   18.9565         0
0  -19.8764   28.1094  -19.8764         0
0   20.8409  -29.4735   20.8409         0
0  -21.8523   30.9038  -21.8523         0
0   22.9128  -32.4035   22.9128         0
0  -24.0247   33.9760  -24.0247         0
```
Nonsense.

:::{warning}
Always obey the First Law of Thermodynamics.
:::

For this class, we will just be aware of this issue. Since the thermal diffusivity is a material property, we don't have control over that in our analyses -- we can, however, choose time and space steps sizes that will ensure a stable numerical solution.