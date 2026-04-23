# Some practice

## Modeling equations

Turn the following into anonymous functions of $x$ and $p$. I'll do one example:

$$
f(t) = A \exp(-bt)
$$

Would be

::::{tab-set}
:::{tab-item} MATLAB
```matlab
f=@(t,p) p(1)*exp(-p(2)*t);
```
:::


:::{tab-item} Python
```python
f=lambda t,p: p[0]*np.exp(-p[1]*t)
```
:::


:::{tab-item} Julia
```julia
f(t,p)= p[1]*exp(-p[2]*t)
```
:::

::::

### Ex 1:
One parameter:

$$
g(u) = 5+10u
$$

### Ex 2:
Three parameters:

$$
\tau(x) = \tau_0 + \mu x^n
$$

### Ex 3:
Three parameters

$$
v(t) = A \cos(\omega t+\phi)
$$


## Converting differential equations into coupled equations for RK4

Turn the following into anonymous functions in terms of $x(1)$, $x(2)$, $x(3)$, $x(4)$, ... . Remember Python/Julia use square brackets, and Python starts from [0]. Worked examples on the [coupled equations page](./8_ODEs/coupled-eqns.md).


### Ex 1:
For known (already defined) parameters $s$, $r$, $b$...

$$
\begin{align}
\dot{x} &= s(y-x)\\
\dot{y} &= x(r-z)-y\\
\dot{z} &= xy-bz\\
\text{with}~x(0)&=x_0,~y(0)=y_0,~z_0=z(0)
\end{align}
$$

### Ex 2:
For known $a$, $b$...

$$
ay'' + b\cos(t) y=\cos(y)
$$

### Ex 3:
For known $m$, $C$, $g$

$$
\begin{align}
m\ddot{x} + C \sqrt{\dot{x}\dot{y}} = 0\\
m\ddot{y} = mg 
\end{align}
$$

### Ex 4:
(We did this one in class on 23 Apr, but you can retry it here.)

$$
y'''+5 y''y -3 y' = \cos(t)
$$

## Discretizing Equations

An example from class:

$$
\frac{\partial u}{\partial t} = a\frac{\partial^2 u}{\partial x^2} + b\frac{\partial u}{\partial x} + x^2
$$

We seek $u(t,x)$ and will need two indices: $i$ to index the time values, and $j$ to index the space locations. Then:

$$
\frac{u_{i+1,j}-u_{i,j}}{\Delta t}= a\frac{u_{i,j+1}-2u_{i,j}+u_{i,j-1}}{(\Delta x)^2} + b\frac{u_{i,j+1}-u_{i,j-1}}{2\Delta x} + x_j^2
$$