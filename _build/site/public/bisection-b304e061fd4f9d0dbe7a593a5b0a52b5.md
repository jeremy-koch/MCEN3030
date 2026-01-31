# The Bisection Method

The Bisection Method is the canonical example of a bracketing method. Assuming that a function $f(x)$ is continuous and that precisely one root exists in a search range $x_L\rightarrow x_U$, it iteratively halves the size of the search range until we say "good enough". So: we might start the search knowing the root is between 0 and 100, a range of 100; after one iteration, we will be able to halve that to 50, after two iterations, 25, ... , after six iterations, we can say with confidence that the root lies within a range of 0.78125. Another way to say that: we pinpoint the root to $x_\text{root}\pm 0.390625$.

:::{note}
Throughout this class, we will often sketch out functions to try to explain/understand algorithms. However, it is usually the case that we don't actually know what the function looks like... otherwise we'd just say "the root is right there!" In the video, we made a sketch, here we will do something a bit more authentic.
:::

## The algorithm

0\. For a given function $f(x)$, we define a search region between $x_L$ ("$x$ lower") and $x_U$ ("$x$ upper"). There must be precisely one root on this range, else the algorithm breaks!  
1\. Calculate $x_M$ ("$x$ middle") as $(x_L+x_U)/2$.  
2\. Calculate $f(x_L)$, $f(x_M)$, and $f(x_U)$ and consider the sign of $f(x_L)\cdot f(x_M)$ OR $f(x_M)\cdot f(x_U)$. (See discussion below about making your code more robust.)  
3a\. If $f(x_L)\cdot f(x_M)< 0$, that means that the function changes sign somewhere between $x_L$ and $x_M$. That is, the root is between $x_L$ and $x_M$.  
4a\. We reset: $x_U=x_M$ and go back to step (1) (where we will use our new definition of $x_U$ to calculate the next $x_M$).

The other possibility is:

3b\. If $f(x_M)\cdot f(x_U)< 0$, that means that the function changes sign somewhere between $x_M$ and $x_U$. That is, the root is between $x_M$ and $x_U$.  
4b\. We reset: $x_L=x_M$ and go back to step (1) (where we will use our new definition of $x_L$ to calculate the next $x_M$).

### An example

What happens for $f(x)=\sin(x)-0.85$? If we are seeking the first root, we know it will exist between $x_L=0$ and $x_U=\pi/2$, and then $x_M=\pi/4$. (We might call $\pi/4$ our initial estimate of the root, and could say: $x_\text{root,0}=\pi/4\pm \pi/4$.)

Let's put it in a table, calling the setup above the zeroth iteration:
```{csv-table}
:header: iteration, $x_L$, $x_M$, $x_U$, $f(x_L)$, $f(x_M)$, $f(x_U)$ 

0, $0$, $\pi/4$, $\pi/2$, $-0.85$, $-0.1428$, $0.15$
```
Since $f(\pi/4)\cdot f(\pi/2)<0$, we know the root is between $x_M$ and $x_U$, so: we reset $x_L=x_M=\pi/4$, keep $x_U=\pi/2$, and calculate a new $x_M=3\pi/8$. (After one iteration, our estimate of the root is $x_\text{root,1}=3\pi/8\pm \pi/8$.) A few more steps:
```{csv-table}
:header: iteration, $x_L$, $x_M$, $x_U$, $f(x_L)$, $f(x_M)$, $f(x_U)$ 

1, $\pi/4$, $3\pi/8$, $\pi/2$, $-0.1428$, $0.0739$, $0.15$
2, $\pi/4$, $5\pi/16$, $3\pi/8$, $-0.1428$, $-0.0185$, $0.0739$
3, $5\pi/16$, $11\pi/32$, $3\pi/8$, $-0.0185$, $0.0319$, $0.0739$
```
... and we could say: after three iterations, our estimate of the root is $x_\text{root,3}=11\pi/32\pm \pi/32$.

### Making the algorithm more robust

We may not actually be certain there is a root within the range we provide, or there may be two roots. In either case, this algorithm fails. It might be a good idea to check the values of both $f(x_L)\cdot f(x_M)$ and $f(x_M)\cdot f(x_U)$ and return an error message if both are $>0$ or both are $<0$.

It is also possible, but unlikely, that ```f(x_L)==0```, or ```f(x_M)==0```, or ```f(x_U)==0```. In any of these cases, the algorithm should promptly end.

Consider the ```break``` or ```return``` commands. See the [coding elements page](../1_prog-basics/coding-elements-overview.md).