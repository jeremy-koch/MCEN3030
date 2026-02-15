# The R2 value

A word about the "R-squared value" that you may have seen, e.g. when plotting a trendline in Microsoft Excel or Google Sheets:

```{figure} r2plot.png
:alt: 
:width: 300px
:align: center

Note the line of best fit equation at the top, $y=17.3x+2.36$, as well as the $R^2$ value, $0.97$. Plot made in Google Sheets.
```

## The "goodness of fit"

The $R^2$ value, also known as the "coefficient of determination", quantifies how good our fit is. We define the quantity as

$$
R^2 \equiv 1-\frac{S_r}{S_t}
$$

where $S_r$ is the sum of the squares of the residuals in our model fit (as defined in the lecture video) and $S_t$ is the sum of the squares assuming the "model" is that the data is constant at the average value of the data set. It can be interpreted as "the fraction of the total variance in the data set that is explained by the model".
:::{hint}
Think about the extremes here. If $R^2 \approx 1$, that implies $S_r\ll S_t$. That is, the model we selected is a much better representation of the data than the model where we just pick the average. If $R^2 \approx 0$, the model we selected is no better than just picking the average value of the data ($S_r\approx S_t$).
:::

What constitutes a "good" value of $R^2$ depends very much on the field of study, and it is of course at the mercy of the accuracy of the data. In the social sciences, where we might be trying to analyze a group of humans with dramatically different backgrounds, an $R^2=0.50$ is pretty good -- there are probably some variables we didn't/couldn't consider, but our model predicted a lot of the variation in the data set. Humans are too complicated!

Meanwhile, in a careful engineering research lab... we'd probably expect an $R^2=0.90$ or so. A well-controlled experiment will have eliminated variables that are difficult to control or quantify and thus the results will have tight error bars.

A common interpretation is that $1-R^2$ should be a measure of the random noise in the data set, and some data sets are just noisier than others. We'll see an example below, though, where this quantity is not noise in the model...

### Overfitting

We always get a "better" $R^2$ value when we add additional parameters to the model. I'll give a cartoonish example: Let's say we have collected some experimental data on the value of $g$ (the acceleration due to gravity) as a function of the oscillation frequency $\omega$ of a pendulum. What should it be? Flat: $g=9.81$ m/s $^2$. 

But suppose there was a bit of a wobble in the data due to experimental error. A model like $g(\omega) = a+b(\omega-c)^2$ might indeed be a "better fit" to the given data, because we have introduced additional parameters $b$ and $c$ that could capture that wobble. But it is nonsense... $g$ should be constant. We would call this "overfitting" or "fitting the error".
:::{seealso}
John von Neumann has a [famous quote](https://en.wikipedia.org/wiki/Von_Neumann%27s_elephant): "With four parameters I can fit an elephant, and with five I can make him wiggle his trunk." He was being critical of his friend for claiming that a model fit the experimental data, pointing out that if you have enough free parameters you can fit anything!
:::

## Can $R^2$ be applied to nonlinear models?

Can it? I guess. Should it? No!

Without getting too deep into statistics, the description we used above -- that the $R^2$-value is the "the fraction of the total variance in the data set that is explained by the model" -- no longer applies when we are considering a nonlinear model. So the conclusions that we draw based on that understanding may be inaccurate: if we try to choose the best nonlinear model based on an $R^2$ calculation, we might actually pick the worst model! If you'd like to read more, [here is a good paper on the subject](https://doi.org/10.1186/1471-2210-10-6).

(There are other "goodness of fit" metrics out there. $R^2$ is just ubiquitous.)

## A case where $R^2$ misleads us

Here is some data, plotted with a linear fit: $\hat{y}=a_0+a_1x + a_2 x^2 + a_3 x^3$. 

```{figure} data_w_fits.png
:alt: 
:width: 300px
:align: center
```

Why guess this model? Cubic equations can decrease, then increase, then decrease, which is maybe(?) what is happening here. At least as far as one-input linear equations go, it's a decent guess. And the $R^2$ value for that model is 0.9826, so it is clearly a good model! Right?

Well... let's make a plot of the residuals at each data point.

```{figure} residuals.png
:alt: 
:width: 300px
:align: center
```

This is concerning! The $R^2$ should be "how much the data is explained by the model", and $1-R^2$, at least for a good model, should be a measure of the random "noise" in the data. Here, we see a clear oscillating "signal" in the error (the residuals) -- it is not noise at all! This is an indication that there is some trend in the data that we are not accounting for. Despite the high $R^2$-value, a different model is needed, maybe a different functional form (square root?) or a nonlinear function.

What we should see in the residuals, if the model is good, is random noise equally distributed around zero. Something like this:

```{figure} residuals_wine.png
:alt: 
:width: 300px
:align: center
```

In this case, we could argue that the model is "good" or "as good as possible", despite $R^2=0.36$, because there are no clear patterns in the error -- it is just noise. The model explains about 36% of the data, 64% is random noise, and that's just how it as. (I am sure there are deeper analyses than "just look at it" though!)

:::{note}
Your homework may have "signal" in the residuals -- we won't get hung up on that. More serious data science efforts might try other models, seek other variables, or bring in machine learning to help develop a more mature understanding of the data.
:::

:::{seealso}
This lesson was inspired by Jim Frost, who has [a great website that talks about issues in statistics](https://statisticsbyjim.com/regression/choose-linear-nonlinear-regression/). If you'd like to read more, click around on his website.
:::