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
R^2 \equiv \frac{S_t-S_r}{S_t}
$$

where $S_r$ is the sum of the squares of the residuals in our model fit (as defined in the lecture video) and $S_t$ is the sum of the squares assuming the "model" is that the data is constant at the average value of the data set. It can be interpreted as "the fraction of the total variance in the data set that is explained by the model".

What constitutes a "good" value of $R^2$ depends very much on the field of study, and it is of course at the mercy of the accuracy of the data. In the social sciences, where we might be trying to analyze a group of humans with dramatically different backgrounds, an $R^2=0.55$ is pretty good -- there are probably some variables we didn't/couldn't consider, but our model predicted most of the variation in the data set. Humans are too complicated!

Meanwhile, in a careful mechanics experiment in the lab... we'd probably expect an $R^2=0.90$ or so. A well-controlled experiment will have eliminated variables that are difficult to control or quantify and thus will have tight error bars. Hopefully the model that we use will describe the data really well, and so $R^2$ should be close to 1.

## For Nonlinear Models



## Simple vs Complex Models and "Overfitting"





## Frequently Asked Questions


### Can $R^2$ be negative?

Yes! We can apply an inappropriate model to a data set.



### My $R^2$ is better with this more complicated model... does that mean more complicated models are better?

Back to linear regression... in modeling a data set, we might consider adding complexity to our model, e.g. going from

$$
f(x_1,x_2)=a_0 + a_1 x_1 + a_2 x_2 \quad\text{to}\quad g(x_1,x_2)=a_0 + a_1 x_1 + a_2 x_2 + b_1 x_1^2 + b_2 x_2^2 + c_{12} x_1 x_2
$$

Both of these [are linear models](lin-or-nonlin.md), and, owing to the extra detail in the second equation, we would likely find that $g$ has a larger $R^2$-value. Does that mean $g$ is the better model?

Probably not. As we increase the complexity of the model, there is a tendency for the model to "fit the error", meaning it sees significance in the experimental error and makes sure that the curve bends to include that erroneous data. That will lead to a better $R^2$-value for the current data set, but that departure from the truth should not be meaningful -- the next time we pass through that data point, that error is probably not going to be there, so let's not design for it. We call this "overfitting".

I'll give a cartoonish example. Suppose we have designed an experiment that measures the force of gravity via a pendulum, and we rush through a set of experiments and get the following.

Wow, massive breakthrough! Gravity is a nonmonotonic function of pendulum length. Call Alfred Nobel.

What is more likely? Experimental error. It should be a flat line at $9.81~\text{m/s}^2$. 



### Can $R^2$ be applied to nonlinear models?

Can it? I guess. Should it? No!

We can calculate it based on the equation above, and actually Microsoft Excel and Google Sheets are really excited to tell you the value:

```{figure} r2nonline.png
:alt: 
:width: 300px
:align: center

The fit equation is $y=58\exp(0.097x)$ and $R^2=0.904$. Good?
```

There are a lot of smart folks working at these companies, they wouldn't lead us astray, would they? They are indeed leading everyone astray.

Without getting too deep into statistics, the description we used above -- that the $R^2$-value is the "the fraction of the total variance in the data set that is explained by the model" -- no longer applies when we are considering a nonlinear model. So the conclusions that we draw based on that understanding may be inaccurate: if we try to choose the best nonlinear model based on an $R^2$ calculation, might might actually pick the worst model! If you'd like to read more, [here is a good paper on the subject](https://doi.org/10.1186/1471-2210-10-6).