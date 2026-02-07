# Linear Modeling

Model fitting is arguably another "matrix method" wherein we are finding the best solution to an over-determined system. It also includes considerations of statistics: is the best solution actually a good solution? Should we try a different model?

This is a topic that I really enjoy, partially because it got me a PhD. Here is a figure from my dissertation:

```{figure} hanoglass.png
:alt: 
:width: 100%
:align: center

For a granular material (here, mm-sized glass beads in silicone oil), he stress necessary to create flow increases with depth. However, at least at slow speeds, vibrating the mixture causes a dramatic reduction in the required stress. Data is plotted with discrete symbols, the lines are best fits from a modeling equation. 
```

The above is technically a nonlinear model -- we will cover both linear and nonlinear modeling and will choose a mathematical path that is similar for both approaches. This page is about linear modeling, though the discussion about "residuals" and "modeling" is useful for both.

## The Residual and "Models"

We quantify the difference between experimental data and a chosen model with "the residual", defined at each data point as $e_i = y_i - \hat{y}(x_i, ...)$. Those symbols are: $e_i$, the residual at data point $i$; $y_i$, the experimental output at point $i$; and $\hat{y}(x_i,...)$, the model prediction at input $x_i$. I include the $...$ because it may be the case that the output depends on several inputs, e.g.: the lift force depends on the speed and the angle of attack.

What do we mean by a "model"? For our purposes: when examining data, we might have reason to believe it can be described by a certain equation. This could be a "just look at it, it's obviously a square root" situation, and that is sometimes useful: even if we can't really justify why it is a square root, we can fit the data and then deal with a simple equation as we go through an engineering design. But it also could be that we have a physical explanation why it would have a certain functional form. Those physics-based equations often have parameters in them that can't be derived -- we need an experiment to figure them out. In the figure above, the model was derived assuming the existence of a modulus, a critical size, a viscosity, and a critical frequency, but the values of those four parameters depend on the specifics of the situation.
:::{seealso}
Here is the paper I got the model from, by the way: [Hanotin et al. "Viscoelasticity of vibrated granular suspensions
", Journal of Rheology (2015)](https://doi.org/10.1122/1.4904421).
:::

With a model selected and the residual calculated at each data point, we can quantify the overall goodness of fit by calculating

$$
S_r \equiv \sum (y_i - \hat{y}(x_i,...))^2
$$

the sum of the residuals (squared). 

The spirit of this unit is: if we have a modeling equation like $\hat{y}=a+bx$, what are the values of $a$ and $b$ that best represent the data? We try out all the different combinations of $a$ and $b$ and the best fit is the pair that has the lowest value of $S_r$.

Actually, we aren't going to "try out all the different combinations" -- we will have a systematic way of doing the calculation that provides the best fit, using matrix math.

## A summary of the math

### Collecting the residuals in a vector

We will use a vector/matrix approach. The experimental outputs will be collected in a column vector $\mathbf{Y}$; the model predictions will be collected in $\mathbf{\hat{Y}}$; and the model itself will be represented by $\mathbf{ZA}$, with $\mathbf{Z}$ being a tall, slender matrix that includes the experimental inputs $(x_i,...)$ and $\mathbf{A}$ a column vector that includes the parameter values to be determined. We can then calculate a vector of residuals as $\mathbf{E}\equiv \mathbf{Y}-\mathbf{\hat{Y}} = \mathbf{Y} - \mathbf{ZA}$ -- an example is below.
:::{note}
The video includes a very basic example, $\hat{y}=a+bx$. Let's do a slightly more complicated example, but the indexing and labeling might get a bit crazy! Let's say the data includes two inputs and one output, $y(x_1,x_2)$, and the model is $\hat{y} = a + b x_1 + c x_2  + d x_1 x_2$. We will use a second index to denote the experiment number, so $x_{1,15}$ is the value of $x_1$ for data point 15.
:::

$$
\begin{bmatrix}
e_1 \\ e_2 \\ e_3 \\ ...
\end{bmatrix}
\equiv
\begin{bmatrix}
y_1 \\ y_2 \\ y_3 \\ ...
\end{bmatrix}
-
\begin{bmatrix}
1 & x_{1,1} & x_{2,1} & x_{1,1}x_{2,1}\\
1 & x_{1,2} & x_{2,2} & x_{1,2}x_{2,2}\\
1 & x_{1,3} & x_{2,3} & x_{1,3}x_{2,3}\\
... & ... & ... & ...
\end{bmatrix}
\begin{bmatrix}
a \\ b \\ c \\ d
\end{bmatrix}
$$

:::{hint}
If the model can't be encapsulated in $\mathbf{ZA}$, it is not a linear model.
:::

### Working with $\mathbf{E}$

:::{warning}
Some vector witchcraft incoming...
:::

We have column vector $\mathbf{E}$, and if we pre-multiply this by its transpose, we get

$$
\mathbf{E}^T\mathbf{E} = e_1^2 +e_2^2 +e_3^2 + ... = S_r
$$

... the sum of the squares of the residuals. That is, the thing we are trying to minimize with respect to our parameters $(a,b,c,d)$. To write this in terms of those parameters, we substitute in $\mathbf{Y} - \mathbf{ZA}$:

$$
S_r = (\mathbf{Y} - \mathbf{ZA}$)^T(\mathbf{Y} - \mathbf{ZA}.
$$

To spare you a bit of the math: we FOIL this, more-or-less like we did in regular algebra (but paying some attention to the transposes), and then take the derivative with respect to $\mathbf{A}$, more-or-less like we did in calculus when trying to find the minimum with respect to a variable (though the vector-ness allows us to compactly do that for all four parameters: $\partial S_r/\partial a, \partial S_r/\partial b, \partial S_r/\partial c, \partial S_r/\partial d$). 

### The final step

Setting the result equal to zero and rearranging, we get

$$
\mathbf{Z}^T\mathbf{Z}\mathbf{A} = \mathbf{Z}^T\mathbf{Y}. 
$$

noting that $\mathbf{Z}$ and $\mathbf{Y}$ are known from our experimental data and model choice, the unknown in this equation is $\mathbf{A}$ -- that is, solving this, using matrix techniques, will yield the best fits for $(a,b,c,d)$ (for this model).


## The algorithm

1. Pick a model. If it is a linear model, proceed with the following.
2. Use the model and your experimental data to build $\mathbf{Z}$. (Also, your experimental data outputs should be collected in a column vector $\mathbf{Y}$.)
3. Determine the best fits to that model via $\mathbf{A} = (\mathbf{Z}^T\mathbf{Z})^{-1}\mathbf{Z}^T\mathbf{Y}. 
4. (Optional) Plot the data and the model fits and judge if it was a good model selection. If it doesn't look good, find a different model -- maybe one with an extra variable in it, or a different combination of variables, or maybe a nonlinear model.


## Next steps

We will talk about nonlinear models. The vocabulary is quite similar, but our $\mathbf{Z}$ matrix in that case is going to be filled with partial derivatives and we are going to need to use an iterative process