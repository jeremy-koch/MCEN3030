# A few probability distributions

... and how to get them in your programming environment.

## Discrete Models

### [Bernoulli](https://en.wikipedia.org/wiki/Bernoulli_distribution)

Probability of a single event, with a Boolean result. Engineering example: a system experiences occasional small power surges slightly above limit of a fuse. Will the fuse blow?

### [Binomial](https://en.wikipedia.org/wiki/Binomial_distribution)

Repeated Bernoulli experiments. A manufacturing process is known to have a defect rate of 2%. What is the probability that there are 10 defects produced in a batch of 100?

### [Poisson](https://en.wikipedia.org/wiki/Poisson_distribution)

The probability of having a certain number of events occur within a certain amount of time, given a known average rate that they happen. A belt typically fails after 1000 hours of use. What is the probability that three belts fail in 800 hours?


## Continuous Models 




### [Uniform](https://en.wikipedia.org/wiki/Continuous_uniform_distribution)

Equal probability within bounds. A machinist is tasked with producing a shaft with diameter between 1.1 and 1.2 cm... the distribution of the acceptable shafts might then be uniform between those limits.


### [Normal (Gaussian)](https://en.wikipedia.org/wiki/Normal_distribution)

The most important distribution, sometimes called "the bell curve". Includes as parameters the mean and variance. Error is usually understood through this lens.

### [Exponential](https://en.wikipedia.org/wiki/Exponential_distribution)

The distance/time between events. A phenomenon occurs at a certain rate. One just happened -- what is the probability another one happens in 1 minute, or 5 minutes?

### [Weibull](https://en.wikipedia.org/wiki/Weibull_distribution)

Useful for time-to-failure.


### [Log-normal](https://en.wikipedia.org/wiki/Log-normal_distribution)

Multiplicative processes, e.g.: many small cracks converge to become big cracks.

### [Gamma](https://en.wikipedia.org/wiki/Gamma_distribution)

Accumulation. Probability of the time until a certain number of events occur, or the total amount of something over time.

### There are more!

Beta, Pareto, Negative Binomial, ...


## Getting them in your language

::::{tab-set}
:::{tab-item} MATLAB
Details on [discrete distributions](https://www.mathworks.com/help/stats/discrete-distributions.html?s_tid=CRUX_lftnav) and [continuous distributions](https://www.mathworks.com/help/stats/continuous-distributions.html?s_tid=CRUX_lftnav) are linked. Might require the Statistics and Machine Learning Toolbox, but then you can access the probability density function (pdf, probability of a given value), cumulative distribution function (cdf, probability below a given value), and obtain a random number from the distribution (rnd) in a similar fashion for each. E.g.:
```matlab
y = wblpdf(x,lambda,k);
z = wblcdf(x,lambda,k);
r = wblrnd(lambda,k,N,1);
```
For uniform and normal distributions, I just use [```rand```](https://www.mathworks.com/help/matlab/ref/double.rand.html) and [```randn```](https://www.mathworks.com/help/matlab/ref/double.randn.html). This uniform distribution is from 0 to 1 and the average of this normal distribution is zero, but you can change those with algebra: e.g., a random number from a uniform distribution between 5 and 10 would be ```5+5*rand()```.
:::


:::{tab-item} Python
All are included in the [scipy.stats package](https://docs.scipy.org/doc/scipy/reference/stats.html), and then you can access the probability density function (pdf, probability of a given value), cumulative distribution function (cdf, probability below a given value), and obtain a random number from the distribution (rvs, "random variates") in a similar fashion for each.
```python
from scipy.stats import bernoulli, binom, poisson, uniform, norm, expon, weibull_min, lognorm, gamma

weibull_min.pdf(x, c=k, scale=lam)
weibull_min.cdf(x, c=k, scale=lam)
weibull_min.rvs(c=k, scale=lam, size=N)
```
:::


:::{tab-item} Julia
The [distributions package](https://juliastats.org/Distributions.jl/stable/) is really interesting and works differently than in MATLAB and Python. Here's an example...
```julia
using Distributions

d = Weibull(k, λ)
pdf(d, x)
cdf(d, x)
rand(d, N)
```
It is like there is a Weibull "class" (apparently it's illegal to talk about classes within Julia but I trust you won't report me), and you create an object in that class with statistical parameters ```k, λ``` (assuming values for those things have been set), stored as ```d```. Then you reference the probability density function (pdf, probability of a given value), cumulative distribution function (cdf, probability below a given value), and can obtain a random number from the distribution (rand) by referencing ```d```.
:::
::::
