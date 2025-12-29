# Intro to ODEs/PDEs

**Author:** Jeremy Koch<sup>1,2</sup> \

## Motivation

You are maybe sensing a theme... a class like fluid mechanics might have you solve
\begin{equation}
    0=\frac{d^2 u}{dz^2}
\end{equation}
subject to two boundary conditions (since it is a second-order differential equation). Integrate twice and you have your functional form for $u(z)$. But what about something like
\begin{equation}
    0=\frac{d^2 x}{dt^2} -\mu (1-x^2)\frac{dx}{dt}+x
\end{equation}
which comes up when studying electrical circuits in vacuum tubes... apparently. That is a nonlinear differential equation, and there is no nice general solution. So... we'll never know how it behaves? Nah, we just need to use a numerical technique!

## The ODE Problem Statement

To put it generically, we might have 



<!-- :::{aside}
https://en.wikipedia.org/wiki/Magnetic-core_memory
::: -->


<!-- ::::{tab-set}
:::{tab-item} MATLAB
```MATLAB
f=@(x) x^2
```
:::
:::{tab-item} python
```python
f=lambda x: x**2
```
:::
:::{tab-item} julia
```julia
f=lambda x: x**2
```
:::

:::: -->