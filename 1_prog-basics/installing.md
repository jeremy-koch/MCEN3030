# Getting going in your language



A few recommendations, if you want them. MATLAB has some special steps because we have a license through the school, though overall the installation process is probably the easiest. 

The other languages are open source, meaning you can follow any online tutorial to get them installed. Python technically can be installed with a graphical user interface (GUI), but I have grown to hate that environment -- I recommend miniconda, as described below. You will need to do a bit of work from the command line. Julia takes some command line work. If you flat-out do not want to do command line stuff, just go with MATLAB, but it makes me feel powerful to do command line stuff!
:::{attention}
I considered giving NO instructions for installing Python/Julia, because these languages may require more careful setup/some maintenance throughout the semester. I want students to be willing and able to handle that themselves! But I relented and give some recommendations here.
:::


## MATLAB

MATLAB is the easiest to get going. As a CU student, you have free access if you create an account using your CU email address. Instructions are [here](https://oit.colorado.edu/software-hardware/software-catalog/matlab) -- use the ones for students, under "How to get it".

Once you have a MathWorks account and have it associated with the school's license, you can choose to download a desktop version of MATLAB, or to access the cloud version of the software. (See the note below about toolboxes before installing!) Students in previous semesters have used both options, and you can hop back-and-forth if you would like, so you can decide what works best for you. I like the immediate access of having MATLAB installed on my machine and I think it runs a bit faster, but you can access your code from any computer if you are using the online version. MATLAB has a GitHub integration that I have not explored yet -- you will need to get your code into GitHub Classroom, and that may be the best way. I will revisit this to give some tips!

The MathWorks site has many tutorials, maybe most notably the "MATLAB OnRamp". [You can find it here](https://matlab.mathworks.com/)... it is an "Online Training".


### Toolboxes

Basic MATLAB is going to be enough for the homework in this class. You can always add toolboxes later, and MATLAB online has them installed by default.

We will do a machine learning project in this class, so do install the machine learning toolbox.

Simulink is used MCEN 4043: System Dynamics. If you'd like to go ahead and install it, you can.






## Python

There are multiple avenues here, and if you are confident enough to find you own way (e.g. with pip), I believe in you.

My recommendation is to [install miniconda](https://www.anaconda.com/docs/getting-started/miniconda/install) -- NOT the full Anaconda (which you can find nearby if you really want to, but I'm not linking it). Anaconda is attractive: it has everything you will need in one install, but also a lot of unnecessary stuff. I grew to hate the navigator and the way it insisted on cross-checking all the packages every time I updated, and so I "downgraded" to miniconda. No sluggish navigator, way fewer packages.

Additionally, I am not fond of the IDEs (Integrated Development Environment) that come with Anaconda. I much prefer [VS Code](https://code.visualstudio.com), which supports Jupyter Notebooks and has a GitHub integration.

### Package management

Miniconda starts with no packages, and so you will have to install these manually. NumPy and matplotlib might be all we need at first. Assuming you are using miniconda, [this page has instructions](https://www.anaconda.com/docs/getting-started/working-with-conda/packages/install-packages). Note that miniconda still uses "conda" in the command line. 
:::{aside}
pip is another option for package management, really it's not that different from conda. If you have reason to go that way, do it, plenty of tutorials around.
:::

:::{seealso}
[Seaborn](https://seaborn.pydata.org/examples/index.html) is built on-top of matplotlib... it is beautiful, I recommend installing it too.
::: 

:::{tip}
Many serious programmers insist each project should have its own "environment" with a unique set of packages. For example, TensorFlow apparently does not play nice with NumPy version 2.0 or higher, and so folks who use TensorFlow will likely have an isolated environment for it where NumPy 1.9x is installed. (I still couldn't get it to work on my machine, but that is besides the point!) For this class, it should not be a big deal to just have the general environment. 

If you do want to create separate environments, e.g., one for your homework repository, one for the machine learning project, you can. From the command line, you would start with something like ```conda create --name homework``` and then ```conda activate homework``` puts you in that environment, and then ```conda install numpy``` would get you numpy in just that environment. You need to install packages in each environment -- if you have three environments set up on your machine, you might technically have numpy installed three times.
:::



## Julia

Though this is not as mainstream, there are plenty of tutorials/discussions online from a dedicated and helpful group of users. If you are the type who would be interested in Julia, I assume you will be able to figure it out. Go [here](https://julialang.org), and the [recommended IDE is again VS Code](https://www.julia-vscode.org). There is a [built-in package manager](https://docs.julialang.org/en/v1/stdlib/Pkg/) -- Plots.jl might be all you need to add at the beginning. There is [a debugger](https://www.julia-vscode.org/docs/stable/userguide/debugging/).

Though Julia is technically a compiled language, working within VS Code makes it not feel compiled, which is nice. Something about [just in-time compilation](https://en.wikipedia.org/wiki/Just-in-time_compilation).