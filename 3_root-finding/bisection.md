# The Bisection Method

The Bisection Method is the canonical example of a bracketing method. Assuming that a function $f(x)$ is continuous and that precisely one root exists in a search range $x_L\rightarrow x_U$, it iteratively halves the size of the search range until we say "good enough". So: we might start the search knowing the root is between 0 and 100, a range of 100; after one iteration, we will be able to halve that to 50, after two iterations, 25, ... , after six iterations, we can say with confidence that the root lies within a range of 0.78125. Another way to say that: we pinpoint the root to $x_\text{root}\pm 0.390625$.

:::{note}
Throughout this class, we will often sketch out functions to try to explain/understand algorithms. However, it is usually the case that we don't actually know what the function looks like... otherwise we'd just say "the root is right there!"
:::

## The algorithm

0\. For a given function $f(x)$, we define a search region between $x_L$ ("$x$ lower") and $x_U$ ("$x$ upper"). There must be precisely one root on this range, else the algorithm breaks!  
1\. Calculate $x_M$ ("$x$ middle") as $(x_L+x_U)/2$.  
2\. Calculate $f(x_L)$, $f(x_M)$, and $f(x_U)$ and consider the sign of $f(x_L)\cdot f(x_M)$ OR $f(x_M)\cdot f(x_U)$. (See discussion below about making your code more robust.)  
3\. (a) If $f(x_L)\cdot f(x_M)< 0$, that means that the function changes sign somewhere between $x_L$ and $x_M$. That is, the root is between $x_L$ and $x_M$.  
4\. We reset: $x_U=x_M$ and go back to step (1) (where we will use our new definition of $x_U$ to calculate the next $x_M$).

The other possibility is:

3\. (b) If $f(x_M)\cdot f(x_U)< 0$, that means that the function changes sign somewhere between $x_M$ and $x_U$. That is, the root is between $x_M$ and $x_U$.  
4\. (b) We reset: $x_L=x_M$ and go back to step (1) (where we will use our new definition of $x_L$ to calculate the next $x_M$).

### Making the algorithm more robust

We may not actually be certain there is a root within the range we provide, or there may be two roots. In either case, this algorithm fails. It might be a good idea to check the values of both $f(x_L)\cdot f(x_M)$ and $f(x_M)\cdot f(x_U)$ and return an error message if both are $>0$ or both are $<0$.

It is also possible, but unlikely, that ```f(x_L)==0```, or ```f(x_M)==0```, or ```f(x_U)==0```. In any of these cases, the algorithm should promptly end.

Consider the ```break``` command... here is a toy example that you might adapt:
::::{tab-set}
:::{tab-item} MATLAB
```matlab
a=5;
while a<10
    if a==5
        break; % Exit the loop immediately
    end
    a=a+1;
end
```
:::
:::{tab-item} Python
```python
a = 5
while a < 10:
    if a == 5:
        break  # Exit the loop immediately
    a += 1
```
:::
:::{tab-item} Julia
```
a = 5
while a < 10
    if a == 5
        break  # Exits the loop immediately
    end
    global a += 1
end
```
:::
::::

## Comparison to "brute force"

Added soon...