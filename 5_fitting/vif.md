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

Just diving in, I calculate:  and . This model has an , great.

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

Now we find:  and ... a fairly substantial change in the fit values!

We are hinting at a truth: if there is uncertainty in the data there is uncertainty in the model fits. It is not necessarily true that all two-parameter models have this dramatic uncertainty -- what is it about this particular data set that makes the parameter values so sensitive to small changes in the data? And, can we even trust a linear model if a tiny rounding error in the data dramatically changes the values of the parameters? It will lead to big differences in the predictions!

You might notice that there is a correlation between  and , namely . So... what if we just ditched the  variable and tried a model like ?** I find  and  for the first data set and  and  for the second. Much less propagated uncertainty in the fitting parameter value. The takeaway is: when the input variables are correlated, the fitted parameter values have a high level of uncertainty.

The Variance Inflation Factor (VIF) is a metric that can help us determine if the input values are correlated, and then we can decide to eliminate some input variables from our models and proceed forward with a modeling equation that is more robust. Suppose we have a data set  (that is, y is a function of 5 variables). The VIF can be calculated for each input variable according to



where  is the R-squared value when we try to predict the nth variable based on the other input variables in the data set. 

What does that mean? As an example, we would carry out an analysis to fit . So, we investigate if  is a function of the other four input variables (not y, just the input variables). Then we calculate the R-squared value for that modeling effort, and then use that to calculate VIF4. Recalling the reading on the R-squared Value, if  is large, it implies that  is well-predicted by the other variables in the model -- that is, we don't really have  as an independent variable in the data set, it itself is predicted by the other variables in the problem. According to the above equation, VIF4 will have a large value as well. (We use this definition because it describes the amount of statistical variance in the model fit, but let's not get too deep into that!)

If any VIFn value is "large" (and the definition of "large" depends on the context), it is common practice to just eliminate that variable from any ensuing modeling analysis. It is common to say 5 is "large. If VIF4 > 5, we might just drop variable  from our linear model and proceed with . (We also might re-run the VIF analysis after having removed  from the analysis to confirm the remaining variables are not correlated -- you will need to do this on Project 1: wine chemistry.)

 

 

**After all, if  we could rewrite the model as . 