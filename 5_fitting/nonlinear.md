# Nonlinear Modeling

For a model like $\hat{y}=a+bx_b+c x_c$, it is pretty clear how to create a $\mathbf{Z}$-matrix:

$$
\begin{bmatrix}
\hat{y_1}\\
\hat{y_2}\\
...
\end{bmatrix}
=
\begin{bmatrix}
1 & x_{b1} & x_{c1}\\
1 & x_{b2} & x_{c2}\\
...
\end{bmatrix}
\begin{bmatrix}
a\\b\\c
\end{bmatrix}.
$$

But we might encounter a situation in which our model is something like $\hat{y}=b+a\sin(\omega t+\phi)$... an offset (by $b$) sine wave, with amplitude ($a$), frequency ($\omega$), and phase-shift ($\phi$) to-be-determined. You can have a try, but there is no way to frame this in the same way as above. This is a nonlinear model, and we will need to modify our technique.

## Background Math

Very similar to [2D Newton-Raphson](../3_root-finding/NR-2D.md), we are going to use an iterative method in which we calculate how to adjust our guesses for the best-fit parameters until we find convergence. We will look to a higher-dimensional Taylor Series, though this time we are exploring adjustments in the parameters:

$$
\hat{y}(x_i;a,b\omega,\phi) \approx \hat{y}(x_i;a_0,b_0,\omega_0,\phi_0) + \frac{\partial \hat{y}}{\partial a}\bigg\rvert_0 \Delta a + \frac{\partial \hat{y}}{\partial b}\bigg\rvert_0 \Delta b + \frac{\partial \hat{y}}{\partial \omega}\bigg\rvert_0 \Delta \omega + \frac{\partial \hat{y}}{\partial \phi}\bigg\rvert_0 \Delta \phi.
$$

So, notably, the "reference value" for a given data point $i$ will additionally include guesses for the four parameters, and the left-hand-side of the equation above can be interpreted as "approximately how much will $\hat{y}$ change if we modify the parameters by $\Delta a$, $\Delta b$, etc., from the reference values".

## Incorporating in a new Z-matrix

Go back to the definition of the residual, $e_i = y_i - \hat{y}_i$, and substitute-in the Taylor Series from above:

$$
e_i \equiv y_i - \hat{y}(x_i,...) = y_i - \left[\hat{y}(x_i;a_j,b_j,\omega_j,\phi_j) + \frac{\partial \hat{y}}{\partial a}\bigg\rvert_{i,j} \Delta a + ...\right].
$$

(The other three terms should be included but it's going to take up a lot of space so I skipped them.) Anticipating an iterative scheme, we label our current iteration as $j$.  With a slight regrouping, we can incorporate this into a vector form of the residuals, [as we did in the linear modeling cases](linear.md):

$$
\begin{bmatrix}
e_1 \\ e_2 \\ ⋮
\end{bmatrix}
=
\begin{bmatrix}
y_1 -\hat{y}(x_1;a_j,b_j,\omega_j,\phi_j)\\ y_2 -\hat{y}(x_2;a_j,b_j,\omega_j,\phi_j) \\ ⋮
\end{bmatrix}
-
\begin{bmatrix}
\frac{\partial \hat{y}}{\partial a}\bigg\rvert_1 & \frac{\partial \hat{y}}{\partial b}\bigg\rvert_1 & \frac{\partial \hat{y}}{\partial \omega}\bigg\rvert_1 & \frac{\partial \hat{y}}{\partial \phi}\bigg\rvert_1 \\
\frac{\partial \hat{y}}{\partial a}\bigg\rvert_2 & \frac{\partial \hat{y}}{\partial b}\bigg\rvert_2 & \frac{\partial \hat{y}}{\partial \omega}\bigg\rvert_2 & \frac{\partial \hat{y}}{\partial \phi}\bigg\rvert_2 \\
⋮ & ⋮ & ⋮ & ⋮
\end{bmatrix}_j
\begin{bmatrix}
\Delta a \\ \Delta b \\ \Delta \omega \\ \Delta \phi
\end{bmatrix}
$$

We label this as $\mathbf{E} = \mathbf{D}-\mathbf{Z} \cdot\mathbf{\Delta A}$. This should be quite reminiscent of the linear case, and similar vector math ensues: create $\mathbf{E}^T \mathbf{E} = S_r$, and then trying to minimize that with respect to... in this case, $\mathbf{\Delta A}$. 
:::{note}
What's the idea here? We are essentially asking: what values of $(\Delta a,\Delta b,\Delta \omega,\Delta \phi)$ will lead to the greatest reduction in $S_r$. However, that displacement is a slightly imperfect answer to the question because the $\mathbf{Z}$ matrix is linearized based on the starting location -- hence the need for iteration, just as we did with [Newton-Raphson](../3_root-finding/NR-1D.md).
:::

After rearranging (similar to the linear case), the result:

$$
\mathbf{\Delta A}_j= (\mathbf{Z}_j^T\mathbf{Z}_j)^{-1}\mathbf{Z}_j^T\mathbf{D}_j.
$$

where the subscript $j$ is a reminder that this is an interative process. We must re-evaluate $\mathbf{Z}_j$ and $\mathbf{D}_j$ each iteration with our new values $a_{j+1} = a_j+ \Delta a_j$, etc. 

## The algorithm


1. Pick a model. If it is a nonlinear model, proceed with the following.
2. Analytically calculate the partial derivatives of that model with respect to each parameter. These are necessary inputs to the problem. Additionally, we need to provide seed guesses for the paramater values.
3. Use the expressions for the partial derivatives and the current guess to build $\mathbf{Z}_j$ for each experimental point, and use the experimental data and the current guess to build $\mathbf{D}_j$.
4. Improve upon your guess for the parameters via $\mathbf{\Delta A}_j = (\mathbf{Z}_j^T\mathbf{Z}_j)^{-1}\mathbf{Z}_j^T\mathbf{D}_j$.
5. Go back to step 3. Iterate until happy with the convergence.
6. (Recommended) [Plot the data and the model fits](anscomb.md) and judge if it was a good model selection. If it doesn't look good, find a different model.