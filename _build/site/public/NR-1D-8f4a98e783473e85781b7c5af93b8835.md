# The (1D) Newton-Raphson Method

The Newton-Raphson Method is another root-finding algorithm, though this one is called an "open" method because the search is not confined to a specific range. This has it's positives: most notably, it converges more quickly than the bisection method; and negatives: it is not guaranteed to find a solution even if one exists. Another downside: we must analytically calculate the function's derivative in order to implement the algorithm (though we'll also talk about a modified version that doesn't require this). Still, I think it is a beautiful idea, and it is one of the most useful ideas in computational methods!

The idea is this: we have a function for which we are seeking the location where $f(x)=0$, and we have a guess for the solution $x_0$, called the seed (similar to how, with [the Bisection Method](bisection.md) we had to set the search range). We [linearize](../2_foundations/Taylor-Series.md) the function around $x_0$ and trace the resulting line back to $y=0$. If our guess is decent and the function is not too erratic, it is likely that the associated $x$-location (call it $x_1$) is a better estimate of the root than our initial guess. We repeat the process, now linearizing around $x=x_1$ and tracing the line back to find an even better estimate, $x_2$, and then maybe we use that too get an even better estimate, etc.~etc.~etc., until we have acceptably [converged](../2_foundations/error.md). 


## The algorithm

Inputs to the algorithm are: the function ```f``` (defined by an [anonymous function](../1_prog-basics/coding-elements-overview.md)), the function derivative ```fp```, a seed ```x_0```, an [acceptable convergence](../2_foundations/error.md) ```con_accept```, and probably a maximum number of iterations ```max_iter```. The last argument is necessary to halt the program when it is not converging.

Then, a quick derivation: start with the linearized function $f(x) \approx f(x_0)+ f'(x_0)(x-x_0)$ and set $f(x) =0$. Rearrange to solve for $x$, which would be interpreted as "the $x$ such that $y=0$ in the linearized function": $x = x_0 - f(x_0)/f'(x_0)$. This is an iterative scheme, and so we write it with an iterative index $i$:
$$
    x_{i+1} = x_i - \frac{f(x_i)}{f'(x_i)}
$$
This equation is what you will need to program, and the algorithm is quite simple: use the seed $x_0$ to compute the first iteration $x_1$ via the above equation, then use $x_1$ to compute $x_2$, and so on. The program stops when an an [acceptable convergence](../2_foundations/error.md) is met, or when the maximum number of iterations is met.
:::{hint}
For the former... sounds like a ```while``` loop, right? While the convergence metric is bigger than the acceptable convergence value? For the latter, maybe ```break``` or ```return```. See the [coding elements page](../1_prog-basics/coding-elements-overview.md).
:::

### An example
Suppose we want to find the value of $1/\sqrt{c}$ for some known value of $c$. We could reframe this problem as:
$$
    x^2=1/c \implies 1/x^2=c \implies \frac{1}{x^2}-c = 0 = f(x)
$$
and, to perform the algorithm, we will need $f'(x)=-2x^{-3}$. Assembling generally into the algorithm's main equation:
$$
    x_{i+1} = x_i - \frac{1/x^2-c}{-2x^{-3}} \implies x_{i+1} = x_i - \frac{1}{2}\left(c x_i^3 -x_i\right).
$$


To make it concrete, let's choose $c=11$, and we'll need a seed guess... $\sqrt{9}=3$, so how about $x_0=1/3$?

Proceeding: $x_1=0.296296$, $x_2=0.301377$, $x_3=0.301511$, $x_4=0.301511$... it seems we have converged very quickly! The actual answer is 0.301511.
:::{tip}
I did these calculations on [Wolfram Alpha](www.wolframalpha.com) using the "natural language" input: ```x - 1/2*(11* x^3 -x) at x=1/3```, and then changed the ```x=...``` with each iteration.
:::

```{figure} NR_iterations.png
:alt: 
:width: 100%
:align: center

The first and second iterations of Newton-Raphson (red arrows) for $f(x)=x^{-2}-11$ (in blue), beginning with seed $x_0=0.333$. Converges pretty quickly!
```


:::{seealso} Check out...
...this discussion of [the fast inverse square root](https://en.wikipedia.org/wiki/Fast_inverse_square_root) used in the game Quake III. The first step in their algorithm is a mysterious "bit-fiddling technique" (wherein bits stored in a float just change positions), but then they used a Newton-Raphson step to improve the accuracy of the calculation. 
:::