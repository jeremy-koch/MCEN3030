# Runge-Kutta Methods

The Runge-Kutta Methods are a collection of methods for numerically solving ordinary differential equations. Euler's Method is one of them and it uses one term in the time stepping. We are going to focus on a method that uses four terms in the time stepping, and will refer to it is "RK4".

## Idea

We saw in the discussion of [Euler's Method](eulers-method.md) and slope fields that taking a finite, linear step in the direction of the current slope can lead to a significant error in prediction of the next value. There is no consideration of the way that the slope changes in between time points. That is, we need some consideration of the second derivative, in a way. (This is a type of [truncation error](../2_foundations/error.md).)

The problem setup is the same:

$$
\frac{dx}{dt} = f(x,t)\\
x(0)=x_0.
$$

However, instead of immediately drawing a line segment from $(t_i,x_i)$

## Huen's Method (a simpler example)

With Huen's Method, we use a single "predictor": we tentatively use an Euler's Method step forward:

$$
\bar{x}_{i+1}= x_i + \Delta t \cdot f(x_i, t_i)
$$

and then evaluate the slope at that location, $f(\bar{x}_{i+1},t_{i+1})$. Then the actual step forward we take is the average of that slope and the Euler's Method slope. That is: we look forward to see how the slope is going to change, and then modify our actual step forward based on that information.
:::{note}Think
How is this related to the second derivative? And note that we did not actually calculate the second derivative!
:::

Mathematically:
$$
x_{i+1}=x_i + \Delta t\left(\frac{k_1 + k_2}{2} \right)
$$

with

$$
\begin{alignat}{3}
k_1 &= f(x_i,t_i)\\
k_2 &= f(x_i+\Delta t\cdot k_1 , t_i+\Delta t)
\end{alignat}
$$

### Back to RK4

We are going to use a method that has three predictors and the the basic Euler's Method step -- four terms. It looks like this:

$$
x_{i+1}=x_i + \Delta t\left(\frac{k_1 + 2k_2 + 2k_3 + k_4}{6} \right)
$$

with

$$
\begin{alignat}{3}
k_1 &= f(x_i &,t_i &)\\
k_2 &= f(x_i+\tfrac{1}{2}\Delta t\cdot k_1 &, t_i+\tfrac{1}{2}\Delta t &)\\
k_3 &= f(x_i+\tfrac{1}{2}\Delta t\cdot k_2 &, t_i+\tfrac{1}{2}\Delta t &)\\
k_4 &= f(x_i+\Delta t\cdot k_3 &, t_i+\Delta t &)
\end{alignat}
$$

Note that:
- $k_2$ depends on $k_1$
- $k_3$ depends on $k_2$
- $k_4$ depends on $k_3$

and so it is important to evaluate these coefficients in order! Can you see how we are considering the way $f(x,t)$ changes

We are going to implement this method for [coupled and second-order equations](coupled-eqns.md). Hop over to see how.

:::{seealso}
You'll notice that there are weights to the $k$-factors of $1/6$, $2/6$, $2/6$, $1/6$. It is important that the weights sum to $1$, but [there are other options for the weighting](https://en.wikipedia.org/wiki/List_of_Runge–Kutta_methods), including eight-term versions.
:::