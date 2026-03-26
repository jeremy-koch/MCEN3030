# The Shooting Method

[The Runge-Kutta Methods](runge-kutta.md) apply specifically to initial-value problems

$$
\begin{equation*}
\dot{\mathbf{x}} = \mathbf{f}(t,\mathbf{x}) \qquad \text{with}~~\mathbf{x}(0)=\mathbf{x}_0
\end{equation*}
$$

but not all differential equations are initial value problems... for example:

$$
\begin{align*}
&\ddot{y}+\tfrac{1}{10}\dot{y}+\sin(y)=0\\
&~~~~y(0)=\phantom{-}3\\
&~~~~y(L)=-2.
\end{align*}
$$

After [converting this to two coupled first-order equations](coupled-eqns.md):

$$
\begin{align*}
& \dot{y} = z\\
&\dot{z}=-\tfrac{1}{10}z-\sin(y)\\
&~~~~y(0)=\phantom{-}3\\
&~~~~y(L)=-2 ~~~~~\text{(!?)}
\end{align*}
$$

we are stuck -- we don't have an initial condition $z(0)$, so how can we time-step forward using RK4?

## The Shooting Method

The answer is to use the Shooting Method. The idea: we "take aim" by guessing the unknown initial condition and "shoot" using RK4. If we miss the target, the other boundary condition, we adjust our aim. Repeat until we are acceptably close. We will then know what hypothetical initial condition would get us to the correct boundary condition, and can use RK4 one last time to get the correct curve.

Perhaps the trickiest part is: How do we adjust our aim/update our guess for the initial condition? We will use [the Secant Method](../3_root-finding/secant.md).

### Adjusting aim with the Secant Method

Recall that the Secant Method is a root-finding algorithm... we are trying to find the $x$ such that $f(x)=0$. But what is $f$ and what is $x$? (Think about it for a second before reading on.)

Did you think about it?

OK.

For this problem, the function under consideration, the one we are trying to get to zero, is the error between the calculated value at the far boundary (from RK4) and the given boundary condition

$$
\text{err} = y_\text{calc}(L)-y_\text{given}(L).
$$

The thing we are varying as we try to find $\text{err}=0$ is the unknown initial condition, here $z(0)=z_0$.

As it pertains to the secant method:
- Recall that we need to provide two seeds. Let's call them $z_\text{0,1}$ and $z_\text{0,2}$.
- They can be sent through separate RK4 calculations. We are interested in the values at the endpoint, $y_\text{calc,1}(L)$ and $y_\text{calc,2}(L)$. 
- We can calculate two values of error, $\text{err}_1 = y_\text{calc,1}(L)-y_\text{given}(L)$ and $\text{err}_2 = y_\text{calc,2}(L)-y_\text{given}(L)$.
- If $\left|\text{err}_2\right|$ is unacceptably large, we will iterate to get a better guess for $z_0$. The iterative scheme is

$$
z_{0,3}= z_{0,2} - \text{err}_2 \frac{\left(z_{0,2}-z_{0,1}\right)}{\left(\text{err}_2-\text{err}_1\right)}
$$

- Rename: $z_{0,1}=z_{0,2}$, then $z_{0,2}=z_{0,3}$ and $\text{err}_1=\text{err}_2$.
- Iterate until we reach an acceptable error (an input to the algorithm), i.e. until:

$$
\left|\text{err}_2\right| < \text{err}_\text{accept}.
$$


:::{important} Think
We can call RK4 once before the loop, then just once inside the loop (with $\text{err}_1=\text{err}_2$ inside the loop, which is a "fast" calculation). Why?
:::

:::{warning}
Be careful with how you organize and label things -- the example on this page was a differential equation for $y(x)$ and we invented a $z(x)$. RK4 is stated in terms of $x(t)$ with $f(t,x)$. As we stack programs on top of each other and apply them in new applications, it can get tricky!

It is difficult to write a general shooting method function as each problem has different missing information. E.g., we might have been given boundary conditions $\dot{y}(0)$ and $y(L)$, or $y(0)$ and $\dot{y}(L)$. For this reason, the homework problem is just a script. 
:::


:::{seealso}
It is possible to have two+ "missing" initial conditions as well! In such a case we can do a Secant Method version of [2+D Newton-Raphson](../3_root-finding/NR-1D.md).
:::