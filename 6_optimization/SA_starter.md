# Steepest Ascent Starter

The discussion about how to generalize steepest ascent was great! It can be a challenge to figure out how to frame a function such that it works regardless of the dimension, but we can usually find a way. And then we have a more useful program!

It seems like most of us made it to the correct vector description. I wanted to give you these code snippets to make sure we are on the same page, including all the coefficients for the homework problem (so that you don't have to type them yourself). In particular, Python is a little tricky because of the difference between lists and numpy arrays.

::::{tab-set}
:::{tab-item} MATLAB
```matlab
% your driver script will use 
b11=-1.0;
b22=-1.2;
b33=-1.3;
b13= 0.4;
a1=.611;
a2=1.791;
a3=.722;
a0=2.4;

y = @(x) ( ...
      a0 ...
    + a1*x(1)      + a2*x(2)      + a3*x(3) ...
    + b11*x(1).^2  + b22*x(2).^2  + b33*x(3).^2 ...
    + b13*x(1).*x(3) ...
);

grad_y = @(x) [ ...
    something, ...
    something, ...
    something ...
];

% and somewhere within your function you should have
h=@(s) f(x_max+s*grad_f(x_max));
```
:::


:::{tab-item} Python
```python
# your driver script will use
b11 = -1.0
b22 = -1.2
b33 = -1.3
b13 = 0.4
a1 = .611
a2 = 1.791
a3 = .722
a0 = 2.4

y = lambda x: (
      a0
    + a1*x[0]      + a2*x[1]      + a3*x[2]
    + b11*x[0]**2  + b22*x[1]**2  + b33*x[2]**2
    + b13*x[0]*x[2]
)

grad_y = lambda x: np.array([
      something,
      something,
      something
])

# and somewhere within your function you should have
h = lambda s: f(x_max + s*grad_f(x_max))
```
:::


:::{tab-item} Julia
```julia
# your driver script will use
b11=-1.0
b22=-1.2
b33=-1.3
b13=0.4
a1=.611
a2=1.791
a3=.722
a0=2.4

y = x -> (
      a0
    + a1*x[1]      + a2*x[2]      + a3*x[3]
    + b11*x[1]^2   + b22*x[2]^2   + b33*x[3]^2
    + b13*x[1]*x[3]
)

grad_y = x -> [
      something,
      something,
      something
]

# and somewhere within your function you should have
h = s -> f(x_max + s*grad_f(x_max))
```
:::
::::