# The Condition Number (Optional) 

## Nearly parallel equations
By solving the system of equations
$$
a_1x+b_1y = c_1\\
a_2x+b_2y = c_2
$$
we are identifying the location in $(x,y)$-space that satisfies both $a_1x+b_1y = c_1$ and $a_2x+b_2y = c_2$. We can frame this as a matrix equation:
\begin{equation}
\begin{bmatrix}
a_1 & b_1\\
a_2 & b_2
\end{bmatrix}
\begin{bmatrix}
x\\y
\end{bmatrix}
=
\begin{bmatrix}
c_1 \\ c_2
\end{bmatrix}
\end{equation}
and can discuss a few cases:
1. There might be infinitely many solutions, e.g. if equation 2 is a multiple of equation 1. Then all $(x,y)$-pairs that satisfy one of the equations will satisfy both of the equations, and we have infinitely many solutions. The determinant of the matrix is 0.
2. There might be no solutions, e.g. if the lines are parallel but with different intercepts. We can't satisfy both equations at the same time. The determinant of the matrix is 0 here too.
3. There might be one solution. The lines are not parallel, and there will be exactly one location where the lines intersect in $(x,y)$-space -- the solution to the problem. The determinant is not zero.

As a purely mathematical problem: Given some values of $a_1,a_2,b_1,b_2,c_1,c_2$, we can say if zero, one, or many solutions exist, and can say what the solution is if one exists.

## Effect of error

Recall "round-off error": we have a finite number of digits to store our numbers. Is that concerning? Usually no, but there are situations when it can be.

Here is a matrix system:
$$\begin{bmatrix}
1 & -1\\
1.01 & -1
\end{bmatrix}
\begin{bmatrix}
x\\y
\end{bmatrix}
=
\begin{bmatrix}
1\\1+e
\end{bmatrix}.$$
This system represents two lines that are not-quite parallel, with a small difference in their y-intercept that is characterized by $e$ (not 2.718, just a variable describing the uncertainty or error). Whenever $e=0.01$, our solution is $(x,y)=(1,0)$. Whenever $e=0.02$, the solution to the system is $(x,y)=(2,1)$! We change the forcing function by 2% and have a massive. This could be massively consequential in an engineering problem! We are in the business of making predictions, and our predictions here could be dramatically incorrect! What are they paying us for?!
:::{aside}
When we study matrix systems like $Ax=b$, it is typical to call $b$ "the forcing function".
:::


This system is said to be "ill-conditioned".

The Condition Number
The condition number can be thought of, generally, as "How sensitive is a problem to variations in the inputs?" As applied to a matrix equation, the following definition is pretty intuitive: If there is some error in the value of the forcing function such that , we might characterize the effect of this error in a relative sense via:



which can be rearranged to

.

The symbol  is the "norm" of the vector or matrix, ostensibly its length or magnitude (though what that means for a matrix is not clear... we'll discuss below).

We are treading dangerously close to some abstract function space mathematics, and I don't want to get into that. Let's just make this claim: the norm of a vector/matrix, multiplied by the norm of another vector/matrix, must be greater than or equal to the norm of the product of those two vectors/matrices. That is: . We can then describe a worst-case scenario in the above equation, regarding it's sensitivity to variations in the input:

.

This is the matrix condition number, "kappa", and we can determine it in MATLAB via cond(A).

Matrix norms
We haven't defined "the norm"  yet.

Vectors
Let's start with vector norms. For a 3D vector , we, as mechanical engineers, are comfortable talking about its magnitude: . It has an intuitive meaning: if we think of  as displacements in three (continuous) directions, then the magnitude is the total length. But there may be other scenarios in which this number is not meaningful. One example is "the Manhattan Metric" -- if you are driving in New York City, the distance between two points on their grid is not , it is actually something like because we cannot "diagonal" across the grid. This, too, is a perfectly reasonable definition of the vector "magnitude" in that application.

As is tradition, mathematicians have to come up with a new word just to be difficult: "norm" instead of "magnitude", I guess because there is a bit of subtlety to the discussion now. And then they often get specific about the type of norm: the first one mentioned above (the one we are most familiar with) is given the name "the L2 norm" (basically because it involves squares and then square roots, so "2"), and the second is "the L1 norm".

Matrices
A question: How should we assess the magnitude of a matrix? Some reasonable-sounding ideas: maybe we take the absolute value of each entry and add them together. Maybe we square all of the values and then add them and then take the square root of that. Maybe we imagine each row or column as a vector, then find the norm of each, and then average those. I think any of these could make sense depending on the application, though if we dove in to function space mathematics and actually studied the rules, we might find some of these metrics don't meet requirements.

Actually, none of these are the "standard definition of norm", which is basically the L2-norm above, extrapolated to a matrix. For a matrix A, the norm is the square-root of the largest eigenvalue of . Why? There is certainly a rigorous reason, but let's just look at it like this: we ostensibly have squared the matrix by multiplying it by its transpose, and then took the square root of some aspect of that result. If you squint, it is kind of like .

There are indeed other norms out there, but this is the one that we commonly refer to as engineers, and we denote it .

Another example
In the problem above the condition number, as determined by MATLAB's cond(A), is about 402. the determinant is about 10^-2... indeed nearly zero. But there is a subtle difference between "ill-conditioned" and "singular". This can be seen in the following: this matrix



has a determinant of 1 but a condition number of 111039. For , the solution to the system is . For , the solution is . So, again, a small change in the problem leads to an extremely significant change in the solution!

Accurate digits
A rule of thumb: if the entries in  and  are accurate to  digits and the condition number is of magnitude , the solution  is accurate to approximately  digits.