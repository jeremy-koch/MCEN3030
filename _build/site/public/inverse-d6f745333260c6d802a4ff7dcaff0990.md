# Matrix Inverse Note

The LU-decomposition can be used to find a matrix inverse. We know $\mathbf{A}\mathbf{A}^{-1}  = \mathbf{I}$ (where $\mathbf{I}$ is the identity matrix... the diagonal is all ones). Let's see what this calculation could look like for a $3\times 3$, where we write the (to-be-determined) entries of the matrix inverse as $c_{ij}$:
$$
\mathbf{A}\mathbf{A}^{-1}  = \mathbf{I} \rightarrow
    \begin{bmatrix}
        a_{11} & a_{12} & a_{13}\\
        a_{21} & a_{22} & a_{23}\\
        a_{31} & a_{32} & a_{33}
    \end{bmatrix}
    \begin{bmatrix}
        c_{11} & c_{12} & c_{13}\\
        c_{21} & c_{22} & c_{23}\\
        c_{31} & c_{32} & c_{33}
    \end{bmatrix}
    =
    \begin{bmatrix}
        1 & 0 & 0\\\
        0 & 1 & 0\\\
        0 & 0 & 1
    \end{bmatrix}.
$$
This can be reinterpreted as
$$
    \begin{bmatrix}
        a_{11} & a_{12} & a_{13}\\
        a_{21} & a_{22} & a_{23}\\
        a_{31} & a_{32} & a_{33}
    \end{bmatrix}
    \begin{bmatrix}
        c_{11}\\
        c_{21}\\
        c_{31}
    \end{bmatrix}
    =
    \begin{bmatrix}
        1\\
        0\\
        0
    \end{bmatrix}
$$
where, reminder, the $a_{ij}$ are known. Further:
$$
    \begin{bmatrix}
        a_{11} & a_{12} & a_{13}\\
        a_{21} & a_{22} & a_{23}\\
        a_{31} & a_{32} & a_{33}
    \end{bmatrix}
    \begin{bmatrix}
        c_{12}\\
        c_{22}\\
        c_{32}
    \end{bmatrix}
    =
    \begin{bmatrix}
        0\\
        1\\
        0
    \end{bmatrix}
$$
and
$$
    \begin{bmatrix}
        a_{11} & a_{12} & a_{13}\\
        a_{21} & a_{22} & a_{23}\\
        a_{31} & a_{32} & a_{33}
    \end{bmatrix}
    \begin{bmatrix}
        c_{13}\\
        c_{23}\\
        c_{33}
    \end{bmatrix}
    =
    \begin{bmatrix}
        0\\
        0\\
        1
    \end{bmatrix}.
$$


That is, we can determine the $i^\text{th}$ column of the inverse matrix using a forcing function that is mostly zeros, except for the $i^\text{th}$ element, which is 1. This is a great opportunity to use LU-decomposition: we can calculate $\mathbf{L}$ and $\mathbf{U}$ once, and then apply them to the different forcing functions: $[1,0,0,0,...]^T$, $[0,1,0,0,...]^T$, $[0,0,1,0,...]^T$, etc., to determine the columns of the inverse.

To check your work, you can use the built-in commands for inverse:

::::{tab-set}
:::{tab-item} MATLAB
```matlab
A=rand(5,5);
invA=inv(A)
```
To solve a linear algebra problem MATLAB has the "under-divide", which is slightly faster than ```inv(A)``` because it does not explicitly calculate the inverse matrix.
```matlab
A=rand(5,5);
b=rand(5,1);
x=A\b
x2=inv(A)*b % same
```
:::


:::{tab-item} Python
```python
import numpy as np
A = np.random.rand(5, 5)
invA = np.linalg.inv(A)
```
To solve a linear algebra problem, one could use:
```python
import numpy as np
A = np.random.rand(5, 5)
b = np.random.rand(5, 1)
x = np.linalg.solve(A, b)
```
:::


:::{tab-item} Julia
```julia
using LinearAlgebra
A = rand(5, 5)
invA = inv(A)
```
To solve a linear algebra problem Julia has the "under-divide", which is slightly faster than ```inv(A)``` because it does not explicitly calculate the inverse matrix.
```julia
using LinearAlgebra
A = rand(5, 5)
b = rand(5, 1)
x = A \ b
x2 = inv(A) * b # same
```
:::
::::