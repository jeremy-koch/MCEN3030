# Euler's Method

In your differential equations class you might have solved

$$
\frac{d x}{dt}=-x
$$

subject to an initial condition $x(t=0)=x_0$. We can solve that one with pencil and paper, it is a "separable equation". 

But what about something like

$$
F(t)=\frac{d^2 x}{dt^2} -\mu (1-x^2)\frac{dx}{dt}+x
$$

which comes up when studying electrical circuits in vacuum tubes. That is a nonlinear differential equation, and there is no nice general solution. So... we'll never know how it behaves? Nah, we just need to use a numerical technique!

## Slope Fields

In differential equations you might have talked about slope fields:

```{figure} slopes_thy.png
:alt: 
:width: 550px
:align: center

Slope field for $dx/dt = 0.2x(5 - x)$, with theoretical solution for $x(0)=1$.
```

Here, we have 

$$
\frac{dx}{dt} = f(t,x)
$$

with $f(t,x) = 0.2x(5-x)$. (To be clear, there is no $t$-dependence in $f(t,x)$, but we are keeping it general.) At any $(t,x)$ location, we can evaluate $f(t,x)$, and so we know the value of the slope at that location. This is how we build the slope field, and solutions to the differential equation will align with the slope field as they are drawn from an initial condition.

:::{note}
Above we plotted a finite number of slopes, but the true solution will match the slope continuously.
:::

## Euler's Method

Euler's Method can be rationalized by thinking about these slope fields. The difference is, we will take finite steps -- usually small, but necessarily finite -- using the slope at a point to draw a line segment that takes us to our next point. Same function as before, with this "time-stepping" in intervals of $\Delta t=0.5$:

```{figure} slopes_0p5.png
:alt: 
:width: 550px
:align: center

Slope field for $dx/dt = 0.2x(5 - x)$, with theoretical solution in red and Euler's Method solution (with $\Delta t=0.5$) in blue.
```

It is a decent approximation, though differences are apparent. Namely, near $t=0$, the the Euler solution is lower than the true solution, and near $t=5$, the Euler solution is higher.

:::{note} Think
Can you explain these discrepancies by referencing the way the slope is changing in between time steps?
:::

:::{important}
This changing slope consideration motivates our use of an [improved version of Euler's Method](runge-kutta.md).
:::

This trend is more apparent with a larger time step: here it is for $\Delta t=1

```{figure} slopes_1.png
:alt: 
:width: 550px
:align: center

Theoretical solution in red and Euler's Method solution with $\Delta t=1$ in blue.
```

and... why not: here it is for $\Delta t = 2$

```{figure} slopes_1.png
:alt: 
:width: 550px
:align: center

Theoretical solution in red and Euler's Method solution with $\Delta t=2$ in blue.
```

The flip side is that if we choose our time step small enough, the slope does not have an opportunity to change much from point to point. Here is the solution for $\Delta t=0.02$.

```{figure} slopes_0p02.png
:alt: 
:width: 550px
:align: center

Euler solution for $\Delta t=0.02$. Slope field is not plotted because . Technically I asked it to plot the analytical solution in red, but the Euler solution (blue) so perfectly mimics it that it is covering it up.
```

## The algorithm

It's relatively simple: for a problem $dx/dt = f(t,x)$ with $x(0)=x_0$, we are going to "time step" forward, using our current values of $t$ and $x$ to predict the next values of $t$ and $x$, until some prescribed limit.

We will use a constant time step $\Delta t$ (an input to our program), and so the $t$-values are easy:

$$
t_{i+1} = t_i + \Delta t.
$$

The $x$-values can be interpreted geometrically: if we evaluate $dx/dt=f(t_i,x_i)$, that gives us "the change in $x$ for a given change in $t$. Our change in $t$ is just $\Delta t$, so our change in $x$ is just $\Delta x = f(t_i,x_i)\cdot \Delta t$. That is:

$$
x_{i+1} = x_i + \Delta t\cdot f(t_i,x_i).
$$

Don't get too excited to implement it. We are going to immediately discuss an improvement that takes into account the way the slope is changing between time points: a [four-term Runge-Kutta Method](runge-kutta.md).