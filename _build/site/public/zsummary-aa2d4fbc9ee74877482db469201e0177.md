# Summary and some things to think about

**Author:** Jeremy Koch<sup>1,2</sup> \

## Some things to think about...
- If we wanted to find the solution to $\exp(x)=1.85$ (and you didn't know where the $\ln$ button was on your calculator), is the $f(x)$ in our root-finding methods $\exp{x}$?
- Sketch $f(x)=\cos{x}-0.85$. If we try to find the first positive root of this equation using Newton-Raphson, would a seed $x_0=0$ get us there?




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