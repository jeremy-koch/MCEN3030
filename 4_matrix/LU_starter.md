# LU Decomposition Starter

Here are some skeleton codes to get you started

## LU Decomposition

::::{tab-set}
:::{tab-item} MATLAB
```matlab
function [L,U] = LU_decomp(A)
% LU_decomp performs the LU decomposition on a general matrix A using 
%   input:      A= a square matrix
%   outputs:    L= a lower-triangular matrix
%               U= an upper-triangular matrix

n=length(A);    % length of a matrix is its number of columns.

U=A;            % Initialize U as A, though it is not U yet -- must iterate.
L=eye(size(A)); % L has 1s along its diagonal, initialize with "eye"

% Big-picture: we go through elements 2->n in the first column to get an
% intermediate matrix, and then 3->n in the second column ... we will
% use nested for loops.

for i=1:n-1     % row i, multiplied by a scalar, is used to change...
    for j=?:? % ... row j
        k= % the multiplier
        U(?,?)=U(?,?)-k*U(?,?); % make sure not to change the rows before i!
        L(?,?)=k;
    end
end

end
```
:::


:::{tab-item} Python
Don't forget Python indexes from zero!
```python
import numpy as np

def LU_decomp(A):
    # LU_decomp performs the LU decomposition on a general matrix A using 
    #   input:      A= a square matrix
    #   outputs:    L= a lower-triangular matrix
    #               U= an upper-triangular matrix

    n = len(A)    # length of a matrix is its number of columns.

    U = A.copy()           # Initialize U as A, though it is not U yet -- must iterate.
    L = np.eye(A.shape[0]) # L has 1s along its diagonal, initialize with "eye"

    # Big-picture: we go through elements 2->n in the first column to get an
    # intermediate matrix, and then 3->n in the second column ... we will
    # use nested for loops.

    for i in range(n-1):     # row i, multiplied by a scalar, is used to change...
        for j in range(?, ?): # ... row j
            k = ? # the multiplier
            U[?, ?] = U[?, ?] - k * U[?, ?] # make sure not to change the rows before i!
            L[?, ?] = k
            
    return L, U
```
:::


:::{tab-item} Julia
```julia
using LinearAlgebra

function LU_decomp(A)
    # LU_decomp performs the LU decomposition on a general matrix A using 
    #   input:      A= a square matrix
    #   outputs:    L= a lower-triangular matrix
    #               U= an upper-triangular matrix

    n = size(A, 2)    # length of a matrix is its number of columns.

    U = copy(A)       # Initialize U as A, though it is not U yet -- must iterate.
    L = Matrix{Float64}(I, size(A)) # L has 1s along its diagonal, initialize with "eye" (requires `using LinearAlgebra`)

    # Big-picture: we go through elements 2->n in the first column to get an
    # intermediate matrix, and then 3->n in the second column ... we will
    # use a nested for loop.

    for i = 1:n-1     # row i, multiplied by a scalar, is used to change...
        for j = ?:?   # ... row j
            k = ?     # the multiplier
            U[?, ?] = U[?, ?] - k * U[?, ?] # make sure not to change the rows before i!
            L[?, ?] = k
        end
    end

    return L, U
end
```
:::
::::


## Forward-Substitution Algorithm

::::{tab-set}
:::{tab-item} MATLAB
```matlab
function [d] = forward_sub(L,b)
% forward_sub uses the forward-substitution algorithm to solve the equation
% Ld = b for a lower-triangular matrix L
% inputs:   L= a lower-triangular matrix
%           b= a vector "forcing function"
% output:   x= the solution to Ld = b

n=length(b);
d=zeros(size(b));

% Use a for loop that counts from i=1 to n.
% Within that loop, you will need to calculate a new sum each time.
% I recommend re-initializing a variable called S each time, at zero,
% and then computing the sum with another for loop.

end
```
:::


:::{tab-item} Python
```python
import numpy as np

def forward_sub(L, b):
    # forward_sub uses the forward-substitution algorithm to solve the equation
    # Ld = b for a lower-triangular matrix L
    # inputs:   L= a lower-triangular matrix
    #           b= a vector "forcing function"
    # output:   x= the solution to Ld = b

    n = len(b)
    d = np.zeros(b.shape)

    # Use a for loop that counts from i=1 to n.
    # Within that loop, you will need to calculate a new sum each time.
    # I recommend re-initializing a variable called S each time, at zero,
    # and then computing the sum with another for loop.
    
    return d
```
:::


:::{tab-item} Julia
```julia
function forward_sub(L, b)
    # forward_sub uses the forward-substitution algorithm to solve the equation
    # Ld = b for a lower-triangular matrix L
    # inputs:   L= a lower-triangular matrix
    #           b= a vector "forcing function"
    # output:   x= the solution to Ld = b

    n = length(b)
    d = zeros(size(b))

    # Use a for loop that counts from i=1 to n.
    # Within that loop, you will need to calculate a new sum each time.
    # I recommend re-initializing a variable called S each time, at zero,
    # and then computing the sum with another for loop.

    return d
end
```
:::
::::



## Backward-Substitution Algorithm

::::{tab-set}
:::{tab-item} MATLAB
```matlab
function [x] = back_sub(U,d)
% backsub uses the back-substitution algorithm to solve the equation Ux = d
% for an upper-triangular matrix U
% inputs:   U= an upper-triangular matrix
%           d= modified forcing function, as in Ld=b
% output:   x= the solution to Ux = d

n=length(d);
x=zeros(size(d));

% Use a for loop that counts backwards from i=n to 1.
% Within that loop, you will need to calculate a new sum each time.
% I recommend re-initializing a variable called S each time, at zero,
% and then computing the sum with another for loop.

end
```
:::


:::{tab-item} Python
```python
import numpy as np

def back_sub(U, d):
    # backsub uses the back-substitution algorithm to solve the equation Ux = d
    # for an upper-triangular matrix U
    # inputs:   U= an upper-triangular matrix
    #           d= modified forcing function, as in Ld=b
    # output:   x= the solution to Ux = d

    n = len(d)
    x = np.zeros(d.shape)

    # Use a for loop that counts backwards from i=n to 1.
    # Within that loop, you will need to calculate a new sum each time.
    # I recommend re-initializing a variable called S each time, at zero,
    # and then computing the sum with another for loop.

    return x
```
:::


:::{tab-item} Julia
```julia
function back_sub(U, d)
    # backsub uses the back-substitution algorithm to solve the equation Ux = d
    # for an upper-triangular matrix U
    # inputs:   U= an upper-triangular matrix
    #           d= modified forcing function, as in Ld=b
    # output:   x= the solution to Ux = d

    n = length(d)
    x = zeros(size(d))

    # Use a for loop that counts backwards from i=n to 1.
    # Within that loop, you will need to calculate a new sum each time.
    # I recommend re-initializing a variable called S each time, at zero,
    # and then computing the sum with another for loop.

    return x
end
```
:::
::::