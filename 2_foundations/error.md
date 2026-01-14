# Numerical Error

Here we describe numerical error. These are definitions, and not everyone uses precisely the same terminology, but we will try to be consistent in this class.

---

## Quantifying Error

### Absolute error

Error is a fact of life in engineering -- measurement devices are miscalibrated, data is processed according to Bernoulli's Equation but Bernoulli's Equation neglects viscosity, computers can store only finite detail, etc. Regardless of the reason the error emerges, we can describe the relationship between the "true value" and "measured value" with (error)=(true value)-(measured value). We define this measurement of error as the "absolute error".

In some situations it is useful to quantify error in this way. For example, in darts you might have an error of 3 (cm) in regards to the triple 20. That conveys meaningful information about how to adjust your trajectory to hit the target. However, a downside of this metric is that it neglects to consider the magnitudes of the numbers involved: an error of $\pm 1$ is no-big-deal if the values in question are greater than, say, 100, while an error of $\pm 1$ is devastating if the numbers in question are about 1.1. "One away" might be incredibly good if we are talking about a dart missing its target in microns, but it might be awful if we are talking meters.
:::{aside}
The absolute error changes depending on the units being used.
:::

### Relative Error

"Relative error" is often preferred in engineering applications because it conveys information about the size of the numbers in question via a normalization by the trusted/true value:
\begin{equation}
(\text{error}_\text{rel})\equiv \left| \frac{(\text{true value})-(\text{measured value})}{(\text{true value})} \right|.
\end{equation}
We may choose to represent this as a percentage by multiplying it by 100. Then, we have some intuition: a 1% (relative) error is, in most engineering applications, very good, and it doesn't matter if we are talking about something small like the measurement of the diameter of a human hair or something large like the diameter of a sun spot. We understand what a 1% error means and probably have respect for that level of accuracy.

:::{caution}
Problems arise if the true value is zero, and arbitrary placement of the zero point influences this metric: the relative error between 275 and 280 K is fairly small, the relative error between 2 and 7°C is much larger.
:::
:::{tip}
I usually prefer to represent a 1% error as err=0.01 in my code, to avoid having to do the awkward multiplication by 100.
:::

## Accuracy and Precision

Let's describe what we might mean by "accuracy" and "precision" when it comes to storage of numbers. The most common way to store a number in scientific programming is as a "double"/"double-float", with 64 bits of information (in binary). Because of the way these numbers are represented, this corresponds to about 16 (base 10) digits. We might say that the "precision" of such a number (in regards to the storage process), is 16 digits.



Sixteen digits is, in most engineering applications, incredibly precise! Astronomers use AU, astronomical units, to measure distance. The average distance between the Earth and the Sun is 1 AU, or $1.5 \times 10^11$ meters. If our average distance from the Sun was one human-hair diameter larger it would be approximately 1.000000000000001 AU. A double is able to store 1.000000000000001, just barely but it can!

If we use 3.309402940125679 as $\pi$, well that's not very accurate. Accuracy is related to the true value of a number: using 3.14 as $\pi$ is more accurate than 3.309402940125679, but 3.309402940125679 is the more precise number. Storing a number as a double limits its precision, but the double architecture has no effect on the accuracy of the number. Actually, we may not know the true value of the number, and thus might not be able to say anything about its accuracy.
:::{aside}
Regarding this 3.309402940125679: it would be like if you had a very carefully designed experiment that could indeed discern 3.309402940125678 from 3.309402940125679, but there was some sort of miscalibration that gave the wrong value. It was a precise experiment, but not an accurate one.
:::

In cases where we are aware of the true value of a number (let's call it $x$), we can describe the number of accurate digits in the approximation (let's call it $\hat{x}$), as
\begin{equation}
(\text{accurate digits})=-\log_{10}\left|\frac{x-\hat{x}}{x}\right|.
\end{equation}
As an example, using the above numbers for $\pi$ (along with an accurate value of $\pi=3.141592653589793$):
\begin{equation}
-\log_{10}\left|\frac{3.141592653589793-3.309402940125679}{3.141592653589793}\right| = 1.27
\end{equation}
and 
\begin{equation}
-\log_{10}\left|\frac{3.141592653589793-3.14}{3.141592653589793}\right| = 3.30.
\end{equation}
We'd probably round these numbers down to say: 3.309402940125679 has one accurate digit, while 3.14 has three accurate digits.

## Sources of Numerical Error

### Round-off Error

We can express big numbers, e.g. 10^100, and small numbers, e.g. 10^-100, as doubles, no problem. But those doubles have finite precision: 16 digits in base 10. If we multiply together two numbers with 16 sig figs by hand, we would ostensibly have 32 known digits, e.g.:
\begin{equation}
2121212121212121\times 9292929292929292 = 19712274257728799240893786348332.
\end{equation}
The two numbers on the left-hand side of this equation can be perfectly described by a double. Their product can't, and we'd lose the precision of the last 16 digits of that number. The detail of the number lost after a calculation is known as "the round-off error".

In many practical applications, we need not be too concerned with round-off error -- losing the last 16 digits above, leaving $0.1971227425772879\times 10^{32}$... that is still precise enough to be used in any engineering calculation. However, it is possible to "push too far" in some computational algorithms, maybe in an intermediate step, such that the round-off error appreciably affects the calculation.

### Truncation Error

How does a computer calculate something like $\sin\left(0.13\right)$? Computers are very prepared to do arithmetic (addition, multiplication) with floats, but calculating sine, not so much. Recall the [Taylor Series](../9_readings/Taylor-Series.md) for sine: 
\begin{equation}
\sin{x}= x-\frac{x^3}{3!}+\frac{x^5}{5!} - \frac{x^7}{7!} + \dots = \sum\limits_{n=0}^\infty \frac{(-1)^n}{(2n+1)!}x^{2n+1}.
\end{equation}
(We are going to talk about Taylor Series probably 10 times this semester, get ready!) One of the neat things about Taylor Series: we can write any function as a polynomial, and polynomials are just addition and multiplication. Computers are able to do simple arithmetic like this quickly. This is actually how calculators determine the sine of a number.

"Truncation error" refers to the difference between a finite summation and a (possibly hypothetical) summation with infinite terms. If $x=0.1$,
\begin{equation}
\sin{(x)}\approx 0.099833 \approx 0.1 = x.
\end{equation}
That is, the truncation error for the "one-term approximation" is not too bad. But for $x=2$,
\begin{equation}
\sin{(x)}\approx 0.909297 \neq 2 = x.
\end{equation}
So the truncation error for the one-term approximation is bad. We need to keep more terms. If we calculate through the $x^7$ term in the Taylor Series, we get 0.907937... pretty decent.

Note that the truncation error is basically theoretical -- the computer is not aware of the "true value" of $\sin{(0.13)}$, and so is unable to judge whether it is accurate based on an assessment of the truncation error.

## Convergence 

So how can we decide when to stop the summation if we don't know the value it is converging to? We can invent a "convergence criterion" to decide that adding one more term is not worth it.

You spent quite some time on convergent/divergent series in Calculus 2, I'll leave the formality to that class. Practically speaking, we can quantify the convergence with a definition like
\begin{equation}
\left| \frac{S_{n+1}-S_{n}}{S_{n+1}} \right|
\end{equation}
where $S_n$ is the sum of series through $n$ terms. In spirit: whenever the above quantity drops below a certain value, say 0.001, we know that the inclusion of one more term in the summation is probably not going to dramatically change the result. And, assuming the summation is well-behaved, we trust that the term after that is even less significant, and the one after that even less significant, and so on. Thus, we have a condition for stopping our summation.

This practical implementation requires some trust that the series is actually converging: according to the above criterion, the summation
\begin{equation}
\sum\limits_{n=1}^N \frac{1}{n}
\end{equation}
might "look like" it is converging after 175 terms, i.e., the 175th term changes the value of the sum by less than 0.001. However, this sum diverges as $N\rightarrow\infty$.

In 3030, we will use this convergence criterion frequently as we iterate to find approximate solutions to analytically unsolveable problems. For example: ```while con>con_accept``` might make several appearances, and we would read this as: "while the convergence criterion is larger than the acceptable value, continue with the while loop".
<!-- :::{hint}

::: -->