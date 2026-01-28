# LU Decomposition

Many analyses in engineering can be boiled-down to: solve $\mathbf{A}\mathbf{x}=\mathbf{b}$. For a square matrix with a non-zero determinant, the solution is:
$$
\mathbf{x}=\mathbf{A}^{-1}\mathbf{b}
$$
but how do we get the inverse? For small matrices there are formulas available, but computational methods is not about handling small matrices!

The $\mathbf{LU}$ decomposition is essentially a formalized version of Gaussian Elimination -- that technique where you subtract rows from each other until you isolate a single unknown in an equation. This can be used to find a matrix inverse/solve $\mathbf{A}\mathbf{x}=\mathbf{b}$. 

MATLAB/NumPy/Julia use $\mathbf{LU}$ in their calculation of the matrix inverse. We will build-up a similar functionality, without leaning on the built-in version. Row operations!



## LU decomposition

### Summary
We seek the solution $\mathbf{x}$ to 
\begin{equation}\label{A}
    \mathbf{A}\mathbf{x} = \mathbf{b}
\end{equation}
where $n\times n$ matrix $\mathbf{A}$ and forcing function $\mathbf{b}$ are known. Our goal is to use row operations to obtain
\begin{equation}\label{U}
    \mathbf{U}\mathbf{x} = \mathbf{d}
\end{equation}
where $\mathbf{U}$ is an upper-triangular matrix and $\mathbf{d}$ is related to the forcing function. With an upper-triangular matrix, the back-substitution algorithm quickly reveals the solution.


% The vector $\mathbf{d}$ \textit{could} be determined by having $\mathbf{b}$ participate in the row operations via and augmented matrix $\mathbf{A}|\mathbf{b}$). We will take another approach: Suppose there is a matrix $\mathbf{L}$ such that $\mathbf{L}\mathbf{U}=\mathbf{A}$. Then 

% Instead, we will calculate $\mathbf{d}$ once we have 

## LU decomposition
### Upper-triangular matrix $\mathbf{U}$ 
Beginning with the general
\begin{equation*}
\mathbf{A}\equiv
\begin{bmatrix}
a_{11} & a_{12} & a_{13} & a_{14} & a_{15} & ... & a_{1n}\\
a_{21} & a_{22} & a_{23} & a_{24} & a_{25} & ... & a_{2n} \\
a_{31} & a_{32} & a_{33} & a_{34} & a_{35} & ... & a_{3n} \\
a_{41} & a_{42} & a_{43} & a_{44} & a_{45} & ... & a_{4n} \\
a_{51} & a_{52} & a_{53} & a_{54} & a_{55} & ... & a_{5n} \\
⋮ & ⋮ & ⋮ & ⋮ & ⋮ & ⋱ & ⋮\\
a_{n1} & a_{n2} & a_{n3} & a_{n4} & a_{n5} & ... & a_{nn}
\end{bmatrix}
\end{equation*}
we perform a series of row operations to make the first column zero (except for the first entry in the column). This can be achieved via
\begin{alignat*}{2}
    (\text{second row})&\rightarrow (\text{second row})-&&\frac{a_{21}}{a_{11}}(\text{first row})\\
    (\text{third row})&\rightarrow (\text{third row})-&&\frac{a_{31}}{a_{11}}(\text{first row})\\
    (\text{fourth row})&\rightarrow (\text{fourth row})-&&\frac{a_{41}}{a_{11}}(\text{first row})
\end{alignat*}
where the $\rightarrow$ can be interpreted as ``becomes''.
:::{caution}
What happens if $a_{11}=0$, even approximately (e.g., 0.000000017)? We need to rearrange the rows such that this is not the case. This is called pivoting, and we will not really worry about it in this class.
:::

After proceeding through all $n$ rows, we will have developed an intermediate matrix
\begin{equation*}
\mathbf{A'}\equiv
\begin{bmatrix}
a_{11} & a_{12} & a_{13} & a_{14} & a_{15} & ... & a_{1n}\\
0 & a'_{22} & a'_{23} & a'_{24} & a'_{25} & ... & a'_{2n} \\
0 & a'_{32} & a'_{33} & a'_{34} & a'_{35} & ... & a'_{3n} \\
0 & a'_{42} & a'_{43} & a'_{44} & a'_{45} & ... & a'_{4n} \\
0 & a'_{52} & a'_{53} & a'_{54} & a'_{55} & ... & a'_{5n} \\
⋮ & ⋮ & ⋮ & ⋮ & ⋮ & ⋱ & ⋮\\
0 & a'_{n2} & a'_{n3} & a'_{n4} & a'_{n5} & ... & a'_{nn}
\end{bmatrix}.
\end{equation*}
If we proceed similarly with
\begin{alignat*}{2}
    (\text{new third row})&\rightarrow (\text{new third row})-&&\frac{a'_{32}}{a'_{22}}(\text{new second row})\\
    (\text{new fourth row})&\rightarrow (\text{new fourth row})-&&\frac{a'_{42}}{a'_{22}}(\text{new second row})
\end{alignat*}
we will arrive at 
\begin{equation*}
\mathbf{A''}\equiv
\begin{bmatrix}
a_{11} & a_{12} & a_{13} & a_{14} & a_{15} & ... & a_{1n}\\
0 & a'_{22} & a'_{23} & a'_{24} & a'_{25} & ... & a'_{2n} \\
0 & 0 & a''_{33} & a''_{34} & a''_{35} & ... & a''_{3n} \\
0 & 0 & a''_{43} & a''_{44} & a''_{45} & ... & a''_{4n} \\
0 & 0 & a''_{53} & a''_{54} & a''_{55} & ... & a''_{5n} \\
⋮ & ⋮ & ⋮ & ⋮ & ⋮ & ⋱ & ⋮\\
0 & 0 & a''_{n3} & a''_{n4} & a''_{n5} & ... & a''_{nn}
\end{bmatrix}.
\end{equation*}
and can continue with this process until we arrive at 
\begin{equation*}
\mathbf{U}\equiv\mathbf{A}''''''\phantom{.}^{...}\equiv
\begin{bmatrix}
a_{11} & a_{12} & a_{13} & a_{14} & a_{15} & ... & a_{1n}\\
0 & a'_{22} & a'_{23} & a'_{24} & a'_{25} & ... & a'_{2n} \\
0 & 0 & a''_{33} & a''_{34} & a''_{35} & ... & a''_{3n} \\
0 & 0 & 0 & a'''_{44} & a'''_{45} & ... & a'''_{4n} \\
0 & 0 & 0 & 0 & a''''_{55} & ... & a''''_{5n} \\
⋮ & ⋮ & ⋮ & ⋮ & ⋮ & ⋱ & ⋮\\
0 & 0 & 0 & 0 & 0 & ... & a''''''\phantom{.}^{...}_{nn}
\end{bmatrix}\equiv
\begin{bmatrix}
u_{11} & u_{12} & u_{13} & u_{14} & u_{15} & ... & u_{1n}\\
0 & u_{22} & u_{23} & u_{24} & u_{25} & ... & u_{2n} \\
0 & 0 & u_{33} & u_{34} & u_{35} & ... & u_{3n} \\
0 & 0 & 0 & u_{44} & u_{45} & ... & u_{4n} \\
0 & 0 & 0 & 0 & u_{55} & ... & u_{5n} \\
⋮ & ⋮ & ⋮ & ⋮ & ⋮ & ⋱ & ⋮\\
0 & 0 & 0 & 0 & 0 & ... & u_{nn}
\end{bmatrix}.
\end{equation*}
This is the upper-triangular matrix $\mathbf{U}$ that will be useful in the back-substitution algorithm.

### Lower-triangular matrix $\mathbf{L}$
The row operations described above can be made mathematical by a multiplication by
\begin{equation*}
\mathbf{L}\equiv
\begin{bmatrix}
1 & 0 & 0 & 0 & 0 & ... & 0\\
a_{21}/a_{11} & 1 & 0 & 0 & 0 & ... & 0 \\
a_{31}/a_{11} & a'_{32}/a'_{22} & 1 & 0 & 0 & ... & 0 \\
a_{41}/a_{11} & a'_{42}/a'_{22} & a''_{43}/a''_{33} & 1 & 0 & ... & 0 \\
a_{51}/a_{11} & a'_{52}/a'_{22} & a''_{53}/a''_{33} & a'''_{54}/a'''_{44} & 1 & ... & 0 \\
⋮ & ⋮ & ⋮ & ⋮ & ⋮ & ⋱ & ⋮\\
a_{n1}/a_{11} & a'_{n2}/a'_{22} & a''_{n3}/a''_{33} & a'''_{n4}/a'''_{44} & a''''_{n5}/a''''_{55} & ... & 1
\end{bmatrix}
\end{equation*}
as in, $\mathbf{L}\mathbf{U}=\mathbf{A}$. Note that the lower-triangular entries are the same as the multipliers we used in the algorithm to get $\mathbf{U}$. The creation of $\mathbf{L}$ is practically a by-product of generating $\mathbf{U}$.

## The Forward-Substitution Algorithm}
Beginning with Eq.~\eqref{U}, we multiply both sides by $\mathbf{L}$ to obtain
\begin{equation*}
    \mathbf{L}\mathbf{U}\mathbf{x} = \mathbf{L}\mathbf{d}.
\end{equation*}
Since $\mathbf{L}\mathbf{U}=\mathbf{A}$, this reveals that
\begin{equation*}
    \mathbf{L}\mathbf{d}=\mathbf{b}.
\end{equation*}
Because $\mathbf{L}$ is a lower-triangular matrix, determination of $\mathbf{d}$ is relatively straightforward via the ``forward-substitution algorithm''. Framed in terms of a generic lower-triangular matrix with entries $\ell_{ij}$, the first three steps are:
\begin{alignat*}{2}
\ell_{11}d_1 & ~ &&= b_1 \implies d_1 = \frac{1}{\ell_{11}}b_1\\
\ell_{21}d_1 & +\ell_{22}d_2  &&= b_2 \implies d_2 = \frac{1}{\ell_{22}}\left(b_2-\ell_{21}d_1\right)\\
\ell_{31}d_1 & +\ell_{32}d_2+\ell_{33}d_3 &&= b_3 \implies d_3 = \frac{1}{\ell_{33}}\left(b_3-\ell_{31}d_1-\ell_{32}d_2\right)
\end{alignat*}
and generally
\begin{equation*}
    d_i = \frac{1}{\ell_{ii}}\left(
    b_i-\sum_{j=1}^{i-1} \ell_{ij}d_j
    \right).
\end{equation*}
We use this to generate $\mathbf{d}$ from the given forcing function $\mathbf{b}$.

## The Backward-Substitution Algorithm
Beginning with Eq.~\eqref{U}, and since $\mathbf{U}$ is an upper-triangular matrix, and since we known $\mathbf{d}$ after going through the forward-substitution algorithm above, we can determine the solution $\mathbf{x}$ via the backward-substitution algorithm. Framed in terms of a generic upper-triangular matrix with entries $u_{ij}$, for a a matrix with $n$ rows, the first three steps are:
\begin{alignat*}{2}
u_{nn}x_n &= d_n &&\implies x_n = d_n/u_{nn}\\
u_{(n-1)(n-1)}x_{n-1} +u_{(n-1)(n)}x_{n}  &= d_{n-1} &&\implies x_{n-1}=\frac{1}{u_{(n-1)(n-1)}}\left(d_{n-1}-u_{(n-1)(n)}x_{n}\right)\\
u_{(n-2)(n-2)}x_{n-2} +
u_{(n-2)(n-1)}x_{n-1} +u_{(n-2)(n)}x_{n} &= d_{n-2} &&\implies\\
&x_{n-2}=&&\frac{1}{u_{(n-2)(n-2)}}\left(d_{n-2}-u_{(n-2)(n-1)}x_{n-1} -u_{(n-2)(n)}x_{n}\right)
\end{alignat*}
and generally
\begin{equation*}
    x_i = \frac{1}{u_{ii}}\left(
    d_i-\sum_{j=i+1}^{n} u_{ij}x_j
    \right).
\end{equation*}
This expression is mathematically correct, but it's implementation is tricky: this algorithm must proceed \ul{backwards}: $i=n$, then $i=n-1$, etc.
