# Classes

In our [2D Newton-Raphson Method](../3_root-finding/NR-2D.md) code, we could write a function that includes, as inputs, ```(f,g,dfdx,dfdy,dgdx,dgdy,...)``` a lot of little functions (either anonymous or full).

An interesting alternative is to pass one thing called, say, ```F```, that includes within it all of those little functions. (So it would be ```(F,...)``` instead!) Then we could define the model entirely within ```F```, and pass that whole model to a general 2D Newton-Raphson code. This is exactly what we can do with "classes" -- it's going to really clean up our code, everything will be packaged together nicely!

## Classes

Let's just dive-in with an example.

We are going to define a class below called ```LineCircle``` that could be used in a [2D Newton-Raphson Method](../3_root-finding/NR-2D.md) problem -- "find where this line intersects this circle". (I made up the name ```LineCircle```, could have called it ```BroccoliRabe``` and everything would be the same.) The set of properties, constructor, and collection of methods could be modified to apply to any system of two equations, and adding more things to this class would allow us to apply the algorithm to a 3D system (though, unless we are really thoughtful, it would probably require a different Newton-Raphson code).

For our purposes: 
:::{note} properties
:icon: false
... are parameters in the problem. For this problem we will have $m$ and $b$ for the line and $R$ for the radius -- they are just constants.
:::
:::{note} the constructor
:icon: false
... is how we create a new variable that is of this class. Here, we provide values for $m$, $b$, and $R$ when initializing a variable.
:::
:::{note} methods
:icon: false
... are tasks or functions associated with the class. For example, we could have a method that calculated the area of the circle (based on ```R```). Here, we will calculate $f(x,y)$, $g(x,y)$, $\partial f/\partial x(x,y)$, $\partial f/\partial y(x,y)$, $\partial g/\partial x(x,y)$, and $\partial g/\partial y(x,y)$. Additionally, let's go ahead and create the Jacobian Matrix as an additional method, which notably will call on the other methods!
:::

::::{tab-set}
:::{tab-item} MATLAB
Note: class definitions in MATLAB must occur in their own file, similar to how we define functions. The class name must match the file name. Alternatively: it can be defined at the bottom of another file (like a local function).
```matlab
classdef LineCircle
    properties
        m % These three parameters will be
        b % set whenever we create a variable
        R % of this class.
    end
    
    methods
        % the "constructor"
        function obj      = LineCircle(m_in,b_in,R_in)
            % obj is a generic way for the class to
            % reference itself
            obj.m=m_in;
            obj.b=b_in;
            obj.R=R_in;
        end
        
        % and the remaining methods are the tasks we'd
        % like to be built-in to the class
        function f_out = f(obj,x,y)
            % m*x+b-y
            f_out=obj.m*x+obj.b-y; 
        end

        function g_out    = g(obj,x,y)
            % x^2 + y^2 - R^2
            g_out= x.^2+y.^2-(obj.R)^2;
        end

        function dfdx_out = dfdx(obj, x, y)
            % this derivative is just m
            dfdx_out=obj.m;
        end
        
        function dfdy_out = dfdy(obj, x, y)
            % for this problem it's just -1
            dfdy_out=-1;
        end

        function dgdx_out = dgdx(obj, x, y)
            dgdx_out=2*x;
        end

        function dgdy_out = dgdy(obj, x, y)
            dgdy_out=2*y;
        end

    end
end
```
With this class defined (in it's own file called ```LineCircle.m```), we can then create a new variable in this class based on the properties and can access those properties using an ```F.something```. And, usefully, we can pass ```F``` to a function. That is, we can input ```(F,...)``` instead of ```(f,g,dfdx,dfdy,dgdx,dgdy,...)```.
```matlab
F = LineCircle(1,0,1);

[A_F,B_F]=a_fxn(F,1,0)
% unsuppressed for a lazy print

function [A,B]=a_fxn(F,x_0,y_0)
    A=F.dfdx(x_0, y_0);
    B=F.g(x_0,y_0);
end

```

:::


:::{tab-item} Python
With Python, we can have the class definition and script within the same file. With the class defined, we can create a new variable in the class based on the properties using an ```F.something```. And, usefully, we can pass ```F``` to a function. That is, we can input ```(F,...)``` instead of ```(f,g,dfdx,dfdy,dgdx,dgdy,...)```.
```python
class LineCircle:
    def __init__(self, m_in, b_in, R_in):
        """
        The constructor and property definitions. 
        Must use "self" to refer to itself
        """
        self.m = m_in
        self.b = b_in
        self.R = R_in
    
    # the useful functions:
    def f(self, x, y):
        return self.m * x + self.b - y
        
    def g(self, x, y):
        return x**2 + y**2 - self.R**2
        
    def dfdx(self, x, y):
        return self.m
        
    def dfdy(self, x, y):
        return -1
        
    def dgdx(self, x, y):
        return 2 * x
        
    def dgdy(self, x, y):
        return 2 * y

def a_fxn(F, x_0, y_0):
    A=F.dfdx(x_0, y_0)
    B=F.g(x_0,y_0)
    return A, B

# Script Execution
F = LineCircle(1, 0, 1)
A_F, B_F = a_fxn(F, 1, 0)
print(f"A = {A_F}, B = {B_F}")
```
And, again, we can use ```F``` as a function input.
:::


:::{tab-item} Julia
Julia does not have "classes" -- a "structure" serves a similar purpose. I'll be honest... not sure what the difference is, other than this looks inside-out when compared to the other two languages. If you figure out another way let me know!

We will define both the model and function within something called a ```module``` that contains a ```struct``` and the ```function```, and then call it from a script below ```using``` the module name. (The ```.someProject``` is necessary because they are in the same file, I think?)
```julia
module someProject

export LineCircle, a_fxn # things we'd like to use outside this module

struct LineCircle
    m::Float64
    b::Float64
    R::Float64
end

# Define the model functions
f(obj::LineCircle, x, y)    = obj.m * x + obj.b - y
g(obj::LineCircle, x, y)    = x^2 + y^2 - obj.R^2
dfdx(obj::LineCircle, x, y) = obj.m
dfdy(obj::LineCircle, x, y) = -1.0
dgdx(obj::LineCircle, x, y) = 2x
dgdy(obj::LineCircle, x, y) = 2y

function a_fxn(F::LineCircle, x_0, y_0)
    A=dfdx(F, x_0, y_0)
    B=g(F,x_0,y_0)
    return A,B
end

end # of the module

# Script
using .someProject

F = LineCircle(1.0, 0.0, 1.0) # m, b, R
A_F, B_F = a_fxn(F, 1.0, 0.0)
println("A = $A_F, B = $B_F")
```
I encountered a bit of an annoynace... within a single REPL session, the module cannot be overwritten once imported. I just restarted the REPL but there are other workarounds.
:::

::::

:::{hint}
We will probably come back to this structure when solving coupled differential equations, defining different functions in that case.
:::