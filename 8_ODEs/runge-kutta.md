# Runge-Kutta Methods

The Runge-Kutta Methods are a collection of methods for numerically solving ordinary differential equations. Euler's Method is one of them and it uses one term in the time stepping. We are going to focus on a method that uses four terms in the time stepping and will refer to it as "RK4".

## Idea

We saw in the discussion of [Euler's Method](eulers-method.md) that taking a finite, linear step in the direction of the current slope can lead to error in the prediction of the next value. There is no consideration of the way that the slope changes in between time points. (This is a type of [truncation error](../2_foundations/error.md).) 

We will see that there are additional factors used in RK4 that give us an idea of how the slope is changing. We'll use this information to modify the slope of the segment as we move from $(t_i,x_i)$ to $(t_{i+1},x_{i+1})$.





## Huen's Method (a simpler example)

Huen's Method is slightly more complicated than Euler's Method and slightly less complicated than RK4. The problem setup is the same:

$$
\frac{dx}{dt} = f(t,x)\\
x(0)=x_0.
$$

but instead of immediately calculating $x_{i+1}=x_i + \Delta t\cdot f(t_i,x_i)$, we are going to send out a "predictor" that gives us an idea of the slope at the next time step, and then we can use that to adjust our solution's path at the current time step. If the next slope is looking like it will be bigger than the present slope, we'll use a slightly bigger slope than in Euler's Method for our time-stepping. And vice versa.

Actually, our predictor is an Euler's Method step:

$$
\bar{x}_{i+1}= x_i + \Delta t \cdot f(t_i,x_i).
$$

We then evaluate the slope at that location, $f(t_{i+1},\bar{x}_{i+1})$, and the actual step forward we take is the average of that "future" slope and the Euler's Method slope. Mathematically:
$$
x_{i+1}=x_i + \Delta t\cdot \left(\frac{k_1 + k_2}{2} \right)
$$

with

$$
\begin{align}
k_1 &= f(t_i,x_i)\\
k_2 &= f(t_i+\Delta t,x_i+\Delta t\cdot k_1).
\end{align}
$$

:::{important} Think
How is this related to the second derivative? Note that we did not actually calculate the second derivative!
:::

### Onward to RK4

We are going to use a method that has three predictors and the basic Euler's Method step -- four terms. It looks like this:

$$
x_{i+1}=x_i + \Delta t\left(\frac{k_1 + 2k_2 + 2k_3 + k_4}{6} \right)
$$

with

$$
\begin{alignat}{3}
k_1 &= f(t_i                      ,& x_i &)\\
k_2 &= f(t_i+\tfrac{1}{2}\Delta t ,& x_i+\tfrac{1}{2}\Delta t\cdot k_1 &)\\
k_3 &= f(t_i+\tfrac{1}{2}\Delta t ,& x_i+\tfrac{1}{2}\Delta t\cdot k_2 &)\\
k_4 &= f(t_i+\Delta t             ,& x_i+\Delta t\cdot k_3 &)
\end{alignat}
$$

Note that:
- $k_2$ depends on $k_1$, and it is not the same $k_2$ as in Huen's Method
- $k_3$ depends on $k_2$
- $k_4$ depends on $k_3$

and so it is important to evaluate these coefficients in order!

This will be the method we use to solve ordinary differential equations in MCEN 3030. We are going to write a general program that can handle [coupled and second-order equations](coupled-eqns.md). Hop over to see how.

:::{seealso}
You'll notice that there are weights to the $k$-factors: $1/6$, $2/6$, $2/6$, $1/6$. It is important that the weights sum to $1$, but [there are other options for the weighting](https://en.wikipedia.org/wiki/List_of_Runge–Kutta_methods), including eight-term versions. This version is a good all-purpose method... I have never felt the need to look at other options.
:::