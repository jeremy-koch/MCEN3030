# SVD for Image Compression

In [the SVD reading](svd.md) I showed two images: a "full-rank" image, and a "low-rank approximation". Here they are again:
```{figure} svd_LB1.png
:alt: 
:width: 550px
:align: center
```
```{figure} svd_LB2.png
:alt: 
:width: 550px
:align: center

Twilight picture (and made black-and-white) of my neighbors' cat, LB, in full detail (top); and in a low-rank approximation (bottom). The low rank approximation ostensibly requires about 5% of the storage space.
```
For today's class, we will do something similar: analyze the singular values of an image and produce a low-rank approximation.
:::{tip}
If you'd like, you could get some experience with [notebook files](../1_prog-basics/notebooks.md) (though my experience is that they are a little buggy when it comes to image-heavy work). Definitely not a requirement but if you want to spend a moment getting it set up, might be nice.
:::

If you finish early, you can either work on the homework due Friday. Or, assuming we keep up our good "attendance" (in regards to watching videos and participating in class), I will write a few exam practice problems for Thursday. Regarding those problems: they will be more valuable to you if you have recently looked over the function inputs and outputs, and thought about their limitations. Not for a grade, I am not even going to collect the exams. But there will be something else you submit...

## Steps

### Find an image and get some code going.
Can be personal (not too personal though) or just from the internet. We will make it black and white.
:::{warning}
No racism, sexism, drugs, booze, ... . Try to find something that has a big detail (like a cat) and some small details too (like wood grain).
:::

For MATLAB, the following commands should work in base MATLAB.

For python, you will need to ```import numpy``` and ```matplotlib.pyplot as plt```.

For Julia, you will need ```using LinearAlgebra, Images, Plots```.

### Import an image and convert to black and white. 

This will effectively be a matrix of numbers once we get it into our programming environment. Check on the size of the image, as in the number of numbers within the matrix.

Key coding elements:
::::{tab-set}
:::{tab-item} MATLAB
```imread```, ```imshow```, ```rgb2gray```, you may need to do ```img=double(img)/255``` to turn the image into a matrix of doubles.
:::


:::{tab-item} Python
```plt.imread```, this will turn it into grayscale: ```A = np.dot(img[...,:3], [0.2989, 0.5870, 0.1140])```, and you may need to do ```A=A/255.0```.
:::


:::{tab-item} Julia
```load```, ```Gray.```, and to turn it into floats: ```A=Float64.(image_BW)```.
:::
::::



### Perform the Singular Value Decomposition and examine the singular values.

[Code is here](svd.md). Then, if it is not already in this format, get a 1D array of the singular values. Plot those values, normalized by the first value, against index number -- i.e., 1 (or 0) to the length of that array. You might consider doing a semilogx plot, as it will show the details for the big singular values better.

Key coding elements: see the reading, and

::::{tab-set}
:::{tab-item} MATLAB
```diag```, ```semilogx```
:::


:::{tab-item} Python
```plt.semilogx```
:::


:::{tab-item} Julia
Within the ```plot``` command, can set ```xaxis=:log10```.
:::
::::

### You make the call.

Based on the singular value plot, we are going to toss out a substantial fraction of the singular values. Above, I reduced 3024 singular values to 100... let's call that value $k$. I could have probably done fewer. The next steps may take some trial and error.

### Slice your U, S, and V.

We will create truncated/compressed versions of each of these matrices, and then combine them.

::::{tab-set}
:::{tab-item} MATLAB
Here's one: ```S(1:k,1:k)```
:::


:::{tab-item} Python
Here's one, if you've got the original S matrix created: ```S_compressed = S[0:k,0:k]```
:::


:::{tab-item} Julia
Here's one: ```S_compressed = Diagonal(S[1:k])```
:::
::::

### View your results.

Take a look at your low-rank approximation. For our purposes, we are trying to make it so that it is clearly compressed, yet we can still tell what it is. 


::::{tab-set}
:::{tab-item} MATLAB
```imshow```
:::


:::{tab-item} Python
```imshow```
:::


:::{tab-item} Julia
```plo``` then ```display```
:::
::::