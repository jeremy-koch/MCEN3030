# Choosing Your Language



Despite what you may have heard, this is not "a MATLAB course" -- I would describe it as "an applied math course". (Indeed, many of the algorithms we will describe were invented long before computers.) In previous iterations of this course we have insisted that students use MATLAB, with the largest reason being to streamline the student, grader, and instructor experience. There are indeed good reasons to use MATLAB, most notably it is easiest to get set up and it is the most likely to be used in other mechanical engineering courses. If those reasons are compelling to you, use MATLAB. However, some folks might be looking ahead to a career where MATLAB is not the standard and would like to get experience with a language that aligns with their career goals. Or they already have some experience in a different language and would like to keep using it. 

:::{important} So what I am getting at?
I am giving you the opportunity to choose the language you use in this course: you may choose MATLAB, Python, or Julia, and will have thousands of lines of coding experience in that language by the end of the semester. (Other languages: let's talk. But they need to be "scripting" or "scripting-like".)
:::


For all three languages, I have provided
- [a page that includes nearly all necessary coding elements](coding-elements-overview.md) that you may reference as you complete your homework. 
- [a page that has recommendations about how to get these set up](installing.md), though, other than MATLAB, you have a lot of flexibility.  
- an ["AI green light"](../0_details/course-policies.md) on homework assignments, which you should not [misuse](../0_details/responsible-AI.md), but it will help to enable this "polyglot" approach to the course.

:::{warning}
No matter what language you choose, you should be prepared to KNOW things like: whether indexing starts with ```0``` or ```1```, how to find the ```length``` of an array, how to write a ```for``` loop, the character used for comments ```# %``` ..., etc. On the exams, forgetting that Python indexes from ```0``` or that MATLAB requires you to ```end``` loops will lose you points -- do not ask for leniency if you make these mistakes. I am empowering you to learn and use whatever language you want, so learn it!

For this reason, you are strongly encouraged to commit to a language (perhaps after a trial period, if you would like). However, and tentatively, I believe I can make the logistics work even if you decide to switch languages during the semester.
:::


Once you have read through the following and think you are ready to commit to a language, see [the installation recommendations page](installing.md).


## TL;DR:

- Choose MATLAB if you want the easiest installation, or if you just want some direct, explicit, no fuss experience with the language that is (probably going to be) used in MCEN 3047: Data Analysis and MCEN 4043: System Dynamics.
- Choose Python if you want the language with widest use, and if you are not bothered by having to do some setup work.
- Choose Julia if you are thoroughly interested in numerical methods and have an appetite for a more challenging but more powerful language. Probably this will be chosen by just a few advanced users. 
- Other: let's talk.



See a more detailed list of pros and cons below, and talk to me if you want to talk about your options. I would guess 60% of the class will choose MATLAB, 35% will choose Python, and 5% will choose Julia/other. (Again: talk to me about "other".) I will let the class know what the distribution is -- I am sure you are curious!

:::{tip}
From a certain, practical level, these languages are very similar, using ```index:slicing```, ```for```, ```while```, etc. You will be able to understand each other's code and will be pretty capable of switching between languages in the future, if needed. You are not committing for life! And AI can help you translate.
:::

:::{warning}
Note that you are responsible for setting up and maintaining your programming environment, which is easy for MATLAB but is slightly more involved for the other languages. 
:::







Included at the bottom of each of these tabs is an example bit of code that would compute
\begin{equation}
    \sum\limits_{n=1}^N \frac{1}{n^k}
\end{equation}
to give you a feel for what some basic code looks like. If you are curious, I would encourage you to look around online to see how engineers are using these languages. You can also go ahead and look at [the overview of basic coding elements](coding-elements-overview.md).

## Pros/Cons
::::{tab-set}
:::{tab-item} MATLAB
Reasons to choose MATLAB:
- For students it is free.
- Easiest to set up: you can either download MATLAB and run it on your machine, or use MATLAB online.
- MATLAB has traditionally been used in MCEN 3047: Data Analysis and MCEN 4043: System Dynamics. Maybe you don't want to be distracted with another language.
- It is a language for scientists and engineers. Matrix math is just: ```A*x```.
- Indexing starts with 1.
- MATLAB has an excellent built-in debug mode.

Reasons to NOT choose MATLAB:
- While it is 100% free for students, it is not free in the real world: a yearly license for an individual costs $1015.
- Related: some companies do use MATLAB and surely are getting a discount from that per-person price tag, but most companies are not going to want to pay thousands of dollars when there are many free options that can do all the same tasks.
- The one function per file architecture is no fun, but is not a huge deal in this class since we will mostly be writing individual functions.
- MATLAB allows you to be "sloppy" in ways that make serious programmers shake their head. (But at the same time, other languages can seem overly rigorous.)
- Launching it takes a minute.
- I find it annoying that the default is to print every line and a ```;``` must be added to prevent that.

Example code:
```matlab
k=2;
N=50;
S=0;        % initialize the sum at zero
for n=1:N
    S=S+1/n^k;
end
print(S)
```
:::


:::{tab-item} python

Reasons to choose Python:
- For everyone it is free.
- Indenting/whitespace is used instead of end statements, which makes the code look really clean. (However, see the note below about needing to prepend ```np.``` for numpy tools.)
- Python is probably the widest used language for scientific computing, or at least it has the most momentum. It is definitely the widest-used for machine learning.
- It is a language that is used beyond engineering computing and you might appreciate getting some adjacent experience. An example: I accidentally scanned a hundred pages in reverse order, but used [PyPDF2](https://pypdf2.readthedocs.io/) to put them right.



Reasons to NOT choose Python:
- It has become widely used by engineers and scientists (see for example [TrackPy](http://soft-matter.github.io/trackpy/)), but at its core it was not invented for engineers. NumPy/SciPy/matplotlib have been thoroughly developed, but it just less appealing to have to deal with ```np.sin(x)``` instead of just ```sin(x)```. Here is how to get a matrix inverse: ```np.linalg.inv(matrix_a)```.Raising to a power is ```**``` instead of ```^```. Ugh. (Yes, I know you can ```from numpy import sin``` or even ```from numpy import *``` but that is rarely done.)
- Indexing starts with 0, which might annoy you enough to look elsewhere.
- The install process, including package management, is not overwhelming, but it is extra steps that may have to occur in the command window/terminal.
:::{aside}

Example code:
```python
import numpy as np # this will be necessary in almost every function, though not really for this little example

k=2
N=50
S=0            # initialize the sum at zero
for n in 1:N
    S+=1/n**k  # ^ is ** in python

# no end needed!

print(S)
```




:::


:::{tab-item} Julia
Reasons to choose Julia:
- For everyone it is free (open source).
- It is a language developed for scientists and engineers. The code looks like math.
- It is a small, seemingly advanced user base of scientists and engineers, but they seem wise and helpful.
- Indexing starts with 1.
- Among these three languages, it is the most serious computational science language, as in: people on the cutting edge of computational research are choosing it.

Reasons to NOT choose Julia:
- Julia is a compiled language. This means the first time you run a new program, it may be slow. My experience is that this is not a big deal.
- It is the least well-developed of the languages in this list, meaning there are fewer tutorials, fewer third-party programs, and fewer users to help.
- It is not clear if Julia will continue to grow or if it will fade away -- you might become an expert in something that no one cares about in 10 years.
- We will likely not have need to use the truly powerful aspects of Julia, e.g. multiple dispatch.
- It seems that Julia sometimes goes out of its way to name things differently than MATLAB/Python. In MATLAB: ```linspace(0,10,101)``` makes an array with 101 elements. In Python+NumPy it is ```np.linspace(0,10,101)```. In Julia it is ```LinRange(0,10,101)```... OK Julia. This is not a reason not to choose Julia on its own, but if you are talking to MATLAB/Python people it is a little annoyance.
- Julia makes some decisions for computational efficiency that can maybe be frustrating to a less-experienced user. For example: you'll see in the code snipped below that an extra step is necessary because variable "scope" is limited within loops. I am sure there are deep reasons for this.

Example code:
```julia


```
:::






:::{tab-item} Other languages
Contact me.
:::
::::

:::{caution}
Remember our goal is to understand the algorithms, not to use built-in tools. While this rule is mostly about things like ```ode45``` (the default ODE solver in MATLAB, which, to emphasize, is not permitted in this class), there may be occasions where "the pythonic"/"the julian" way of doing something opposes the fundamentals of the algorithm. The biggest example of this will likely be with ```for``` loops. I will try to keep an open mind, but also may require you write in un-optimized code that more clearly demonstrates that you indeed understand the algorithm.
:::


## More Reading

[MATLAB vs. Julia vs. Python](https://tobydriscoll.net/post/matlab-vs.-julia-vs.-python/)

[Why numbering should start at zero](https://www.cs.utexas.edu/~EWD/transcriptions/EWD08xx/EWD831.html) (not sure I agree but, here is a reading)


<!-- https://forem.julialang.org/vinodv/julia-vectors-and-matrices-n2l -->




