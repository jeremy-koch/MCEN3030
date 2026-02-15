# The Variance Inflation Factor (optional)

Suppose we have the following data set to which we are attempting to fit the model $\hat{y}=a_0+a_1 x_1 + a_2 x_2$:


<table style="width: 40%">
  <tr>
    <th>x1</th>
    <td>1.0</td>
    <td>2.0</td>
    <td>3.0</td>
    <td>4.0</td>
    <td>5.0</td>
  </tr>
  <tr>
    <th>x2</th>
    <td>1.1</td>
    <td>2.1</td>
    <td>3.0</td>
    <td>3.9</td>
    <td>5.1</td>
  </tr>
  <tr>
    <th>y</th>
    <td>2.3</td>
    <td>4.0</td>
    <td>6.0</td>
    <td>8.3</td>
    <td>10.0</td>
  </tr>
</table>

Just diving in, I calculate: $(a_0, a_1,a_2)=(0.32,3.02,-1.07)$. This model has $R^2=0.9983$, great.

However, what if the data set had some measurement error/uncertainty? Suppose one y value was just a little bit larger, by 3%:

<table style="width: 40%">
  <tr>
    <th>x1</th>
    <td>1.0</td>
    <td>2.0</td>
    <td>3.0</td>
    <td>4.0</td>
    <td>5.0</td>
  </tr>
  <tr>
    <th>x2</th>
    <td>1.1</td>
    <td>2.1</td>
    <td>3.0</td>
    <td>3.9</td>
    <td>5.1</td>
  </tr>
  <tr>
    <th>y</th>
    <td>2.3</td>
    <td>4.0</td>
    <td>6.0</td>
    <td>8.3</td>
    <td>10.3</td>
  </tr>
</table>

Now we find: $(a_0, a_1,a_2)=(0.09,2.03,0.00)$ and $R^2=0.9961$... a fairly substantial change in the fit values, but still we fit the equation.
:::{attention}
The point of fitting is to understand and predict data. Do we really understand and can we make good predictions if the parameters change wildly in response to a tiny change in the data?
:::

We are hinting at a truth: if there is uncertainty in the data there is uncertainty in the model fits. It is not necessarily true that all three-parameter models have this dramatic uncertainty -- what is it about this particular data set that makes the parameter values so sensitive to small changes in the data?

You might notice that there is a correlation between $x_1$ and $x_2$, namely $x_1\approx x_2$. So... what if we just ditched the $x_2$ variable and tried a model like $\hat{y}=a_0+a_1 x_1$? I find $a_0=0.21$ and $a_1=1.97$, with $R^2=0.9975$, for the first data set; and $a_0=0.09$ and $a_1=2.03$, with $R^2=0.9976$ for the second. Still a bit of a difference between the two fits, but much less. The takeaway is: when the input variables are correlated, the fitted parameter values have a high level of uncertainty.
:::{aside}
If $x_2=x_1$, we could rewrite the original model as $\hat{y}=a_0+(a_1+a_2) x_1 = a_0 + b_1 x_1$ and then fit $a_0$ and $b_1$.
:::

## Mathematical Definition of VIF

The Variance Inflation Factor (VIF) is a metric that can help us determine if the input values are correlated, and then we can decide to eliminate some input variables from our models and proceed forward with a modeling equation that is more robust. Suppose we have a data set $y(x_1,x_2,x_3,x_4,x_5)$ (that is, $y$ is a function of 5 variables). The VIF can be calculated for each input variable according to

$$
\text{VIF} \equiv \frac{1}{1-R_n^2}
$$

where $R_n^2$ is the R-squared value when we try to predict the $n$-th variable based on the other input variables in the data set. 

What does that mean? As an example, we would carry out an analysis to fit $x_4 = c_0 + c_1 x_1 + c_2 x_2 + c_3 x_3 + c_5 x^5$. We are essentially investigating if $x_4$ is a function of the other four input variables (NOT $y$, just the input variables). Then we calculate the $R^2$ value for that modeling effort, and then use that to calculate $\text{VIF}_4$. If $R^2$ is large, it implies that $x_4$ is well-predicted by the other variables in the model -- that is, we don't really have $x_4$ as an independent variable in the data set, it is predicted by the other variables in the problem. According to the above equation, $\text{VIF}_4$ will have a large value as well.
:::{note}
Why use VIF instead of $R^2$? It is closely aligned with the amount of statistical variance in the model parameters, but let's not get too deep into that!
:::

If any $\text{VIF}_n$ value is "large" (and the definition of "large" depends on the context), it is common practice to just eliminate that variable from the ensuing modeling analysis. It is common to say 10 is "large": this implies the associated $R_n^2=0.90$. If $\text{VIF}_4 > 10$, we might consider dropping variable $x_4$ from our linear model and proceed with $y(x_1,x_2,x_3,x_5)$. (One should probably rerun the VIF analysis with this pared-down data set to confirm the remaining variables are not correlated.)
:::{tip}
The trickiest thing is keeping the indices straight after dropping a variable. If your data set originally has 6 columns, 5 inputs and 1 output, and you drop variable 4, now variable 5 is in column 4!
:::

:::{attention}
Someone, someday, will show you a model that has two inputs that are clearly correlated, yet they will treat them as independent. Pay attention and be wary of the ensuing analysis -- their model predictions will have inflated uncertainty!
:::