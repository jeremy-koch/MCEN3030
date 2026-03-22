# Euler's Method

In your differential equations class you might have solved

$$
\frac{d x}{dt}=-x
$$

subject to an initial condition $x(t=0)=x_0$. We can solve that one with pencil and paper, it is a "separable equation": $x(t) = x_0 \exp(-t)$. But what about something like

$$
\frac{d^2 x}{dt^2} -\mu (1-x^2)\frac{dx}{dt}+x=G(t)?
$$

That is a nonlinear differential equation, and there is no nice general solution. So... we'll never know how this equation behaves? Nah, we just need to use a numerical technique!

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

with $f(t,x) = 0.2x(5-x)$. At any $(t,x)$ location, we can evaluate $f(t,x)$, and so we know the value of the slope at that location and hence can draw all those little line segments. Solutions to the differential equation will align with the slope field at every location: place your pencil at the initial condition $x(0)=x_0=1$ and start drawing a trajectory to the right such that the curve is always aligned with the local slope field. In a meaningful way, this is the solution to the differential equation (assuming we can continuously calculate the derivative and draw it accurately). And this is more-or-less how we implement Euler's Method, an approximate solution to the differential equation, the difference being we only evaluate the derivative at a finite number of locations.
:::{aside}
To be clear, there is no $t$-dependence in this example $f(t,x)$, but we are keeping it general.
:::

## Euler's Method

Euler's Method can be rationalized by thinking about these slope fields. We will take finite steps -- usually small, but necessarily finite -- using the slope at one point to draw a line segment that takes us to our next point. Here we will look at the same differential equation as before (true solution in red), with this "time-stepping" in intervals of $\Delta t=0.5$ (plotted in blue):

```{figure} slopes_0p5.png
:alt: 
:width: 550px
:align: center

Slope field for $dx/dt = 0.2x(5 - x)$, with theoretical solution in red and Euler's Method solution (with $\Delta t=0.5$) in blue.
```

So... what is this? We take an initial condition, $x(0)=1$, and evaluate the slope $f(t,x)=0.2(1)(5-1) = 0.8$. We draw a line segment from $(t,x)=(0,1)$ with slope $f(t,x)=0.8$ that extends by an amount $\Delta t=0.5$ to $t=0.5$. We stop, re-evaluate $f(t,x)$, and create a new line segment, again extending $\Delta t =0.5$ to get us to $t=1$. Stop, re-evaluate, and draw; stop re-evaluate, and draw; etc., until we reach our stopping point (here, $t=5$). We have constructed an approximation of the true solution to the differential equation without having to analytically solve the differential equation.

It is a decent approximation, though differences are apparent. Namely, near $t=0$, the the Euler solution is lower than the true solution, and near $t=5$, the Euler solution is higher.

:::{important}
Can you explain these discrepancies by referencing the way the slope is changing in between time steps? This changing slope consideration motivates our use of an [improved version of Euler's Method](runge-kutta.md).
:::

This trend is more apparent with a larger time step: here it is for $\Delta t=1$:

```{figure} slopes_1.png
:alt: 
:width: 550px
:align: center

Theoretical solution in red and Euler's Method solution, with $\Delta t=1$, in blue.
```

and... why not: here it is for $\Delta t = 2$. It's gonna be bad.

```{figure} slopes_2.png
:alt: 
:width: 550px
:align: center

Theoretical solution in red and Euler's Method solution, with $\Delta t=2$, in blue.
```

So, the approximation gets worse as the time step gets larger. The flip side is that it should get better if the time step is smaller. Here is the solution for $\Delta t=0.02$:

```{figure} slopes_0p02.png
:alt: 
:width: 550px
:align: center

Euler solution for $\Delta t=0.02$. Slope field is not plotted because it would basically shade-in the background. I did plot the analytical solution in red, but the Euler solution (blue) so perfectly mimics it that it is covering it up.
```

The slope does not have an opportunity to change much from point to point, and so the Euler solution, with its little line segments, does a very good job approximating the true solution... so much so it covers it up entirely!


## The algorithm

It's relatively simple: for a differential equation $dx/dt = f(t,x)$ with initial condition $x(0)=x_0$, we are going to "time step" forward, using our current values of $t$ and $x$ to predict the next values of $t$ and $x$, until some prescribed limit. We will use a constant time step $\Delta t$ (an input to our program), and so the $t$-values are easy:

$$
t_{i+1} = t_i + \Delta t.
$$

The $x$-values can be interpreted geometrically: if we evaluate $dx/dt=f(t_i,x_i)$, that is "the change in $x$ for a given change in $t$". Our change in $t$ is just $\Delta t$, so our change in $x$ is just $\Delta x = f(t_i,x_i)\cdot \Delta t$. That is:

$$
x_{i+1} = x_i + \Delta t\cdot f(t_i,x_i).
$$

Don't get too excited to implement this just yet! We are going to immediately discuss an improvement that takes into account the way the slope is changing between time points: a [four-term Runge-Kutta Method](runge-kutta.md).