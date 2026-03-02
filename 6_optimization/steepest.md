# Steepest Ascent

The Method of Steepest Ascent 

:::{tip}
You may hear about "Gradient Descent" in machine learning. 
:::



:::{important}
Though we will visualize contour plots in this discussion, i.e. $f(x,y)$, steepest ascent applies to any number of variables. Have you ever calculated a seven-component gradient?!
:::


## Idea 






## Algorithm

This is an iterative method, so we will again start with a seed as our "current guess"  


As we did with [nonlinear fitting](../5_fitting/nonlinear.md), we will calculate a numerical gradient at our current location, based on the derivative approximation

$$
\nabla f\bigg\rvert_0 \approx \left< \frac{f(x_1+h,x_2,...)-f(x_1,x_2,...)}{h},\\
\frac{f(x_1,x_2+h,...)-f(x_1,x_2,...)}{h} \right>
$$

:::{tip} Reminder
The benefit of this approach is that we need not supply analytical equations for each term in the gradient... we only need to supply the equation we wish to optimize.
:::


## Using the Golden Search Method

We will use [the Golden Search Method](golden.md) within our Steepest Ascent code.


### Choosing bounds

Based on the above, 
