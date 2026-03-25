# RK4 Starter Code

Our goal is to write a generic solver that can accept any number of coupled equations. We will use a similar strategy as we did for the gradient array in the [Steepest Ascent problem](../6_optimization/SA_starter.md). The homework problem considers the system

$$
\begin{align}
    \frac{dS}{dt} &= \mu N - \frac{\beta I S}{N} + \omega R - \mu S \\
    \frac{dE}{dt} &= \frac{\beta I S}{N} - \sigma E - \mu E \\
    \frac{dI}{dt} &= \sigma E - \gamma I - (\mu + \alpha) I \\
    \frac{dR}{dt} &= \gamma I - \omega R - \mu R
\end{align}
$$

but your code should work for systems with 1, 2, 3, 4, ... whatever number of equations. 


::::{tab-set}
:::{tab-item} MATLAB
Your RK4 function should look like
```matlab
function [t,x] = RK4(f,x_0,dt,t_final)
    % The key aspect is going to be a for loop
    % that uses the values at step i to set
    % the values at step i+1
end
```
where ```f``` is a horizontal array for our system of differential equations (described below), ```x_0``` is a horizontal array of initial conditions, ```dt``` is the time step $\Delta t$, and ```t_final``` is the stopping time. Your code will create ```t```, a column vector of time values (easy); and the solutions to the differential equations at each time point will be stored in ```x```, a matrix that is as wide as ```x_0``` and as tall as ```t```. Note that the first row of ```x``` is ```x_0```.

Your script will create a system of equations via
```matlab
m=1/2000;
b=0.5;
w=1/150;
s=.2;
g=1/14;
a=.005;
x_0=[390,10,0,0];
N=sum(x_0);
dt=0.01;
t_final=60;


f=@(t,x) [m*N-b.*x(3).*x(1)/N+w*x(4)-m*x(1),...
    b.*x(3).*x(1)/N-s*x(2)-m*x(2),...
    s*x(2)-g*x(3)-(m+a)*x(3),...
    g*x(3)-w*x(4)-m*x(4)];
```
:::


:::{tab-item} Python
Your RK4 function should look like
```python
def RK4(f, x_0, dt, t_final):
    # The key aspect is going to be a for loop
    # that uses the values at step i to set
    # the values at step i+1
    return t, x
```
where ```f``` is a horizontal array for our system of differential equations (described below), ```x_0``` is a horizontal array of initial conditions, ```dt``` is the time step $\Delta t$, and ```t_final``` is the stopping time. Your code will create ```t```, a column vector of time values (easy); and the solutions to the differential equations at each time point will be stored in ```x```, a matrix that is as wide as ```x_0``` and as tall as ```t```. Note that the first row of ```x``` is ```x_0```.

Your script will create a system of equations via
```python
m, b, w, s, g, a = 1/2000, 0.5, 1/150, 0.2, 1/14, 0.005
x_0 = [390, 10, 0, 0]
N = sum(x_0)
dt = 0.01
t_final = 60

f_seir = lambda t, x: [
    m*N - b*x[2]*x[0]/N + w*x[3] - m*x[0], # dS
    b*x[2]*x[0]/N - s*x[1] - m*x[1],       # dE
    s*x[1] - g*x[2] - (m+a)*x[2],          # dI
    g*x[2] - w*x[3] - m*x[3]               # dR
]
```
:::


:::{tab-item} Julia
Your RK4 function should look like
```julia
function RK4(f, x_0, dt, t_final)
    # The key aspect is going to be a for loop
    # that uses the values at step i to set
    # the values at step i+1
    return t, x
end
```
where ```f``` is a horizontal array for our system of differential equations (described below), ```x_0``` is a horizontal array of initial conditions, ```dt``` is the time step $\Delta t$, and ```t_final``` is the stopping time. Your code will create ```t```, a column vector of time values (easy); and the solutions to the differential equations at each time point will be stored in ```x```, a matrix that is as wide as ```x_0``` and as tall as ```t```. Note that the first row of ```x``` is ```x_0```.

Your script will create a system of equations via
```julia
m, b, w, s, g, a = 1/2000, 0.5, 1/150, 0.2, 1/14, 0.005
x_0 = [390.0, 10.0, 0.0, 0.0]
N = sum(x_0)
dt, t_final = 0.01, 60

f_seir(t, x) = [
    m*N - b*x[3]*x[1]/N + w*x[4] - m*x[1],
    b*x[3]*x[1]/N - s*x[2] - m*x[2],
    s*x[2] - g*x[3] - (m+a)*x[3],
    g*x[3] - w*x[4] - m*x[4]
]
```
:::
::::