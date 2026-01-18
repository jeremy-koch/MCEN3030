# Taylor Series Refresher

Suppose we have a complicated function $f(x)$, made of natural logs and arctangents or whatever. Not friendly to deal with. We could reasonably ask the question: if there is another function $\hat{f}(x)$ that has the same value as $f(x)$ at $x=x_0$, and the same value of the first derivative (so the value of $\hat{f}(x)$ is changing just as rapidly as $f(x)$ at $x=x_0$), and the same value of the second derivative (so the rate of change of the rate of change of $\hat{f}(x)$ matches that of $f(x)$), and the same value of the third derivative, and the same value of the fourth derivative, etc., onwards to the infinitieth derivative... well, that sounds like we effectively have the same functional behavior for both $f(x)$ and $\hat{f}(x)$. A function that meets this requirement can usually be constructed:
\begin{align}
\hat{f}(x) &= f(x_0)+ (x-x_0)f'(x_0) + \frac{1}{2!}(x-x_0)^2f''(x_0) + \frac{1}{3!}(x-x_0)^3f'''(x_0) \dots \\
& = f(x_0) + \sum\limits_{n=1}^\infty \frac{1}{n!}(x-x_0)^nf^{(n)}(x_0)
\end{align}
out to infinity terms with $f^{(n)}$ being the $n$th derivative. Importantly, this equivalent function, $\hat{f}(x)$, is a polynomial, and polynomials are easy to deal with! The trade-off, of course, is that there are now infinity terms. We'll see if we can tame that.

This is the Taylor Series for the function $f(x)$, and it is one of the most important ideas in engineering. 




## Linearization

Let's suppose $x-x_0=\epsilon$, where $\epsilon \ll 1$. To make it concrete, let's say $\epsilon=0.1$. What is the value, then, of $(x-x_0)^2 = \epsilon^2$? It is small: 0.01. And $(x-x_0)^3 = \epsilon^3$? Even smaller, 0.001.

This tells us that, presuming our $x$ is near to the reference location $x_0$, and that the function itself is reasonably well-behaved, the successive terms in the Taylor Series become decreasingly significant. That is: we might get a decent approximation of the original function $f(x)$ "near" to the reference point $x_0$ by just using the "linearization"
\begin{equation}
f(x) \approx f(x_0) + (x-x_0)f'(x_0).
\end{equation}
This is the most practical lesson we learn from Taylor Series and will be the foundation for many of the algorithms we use in this course.

