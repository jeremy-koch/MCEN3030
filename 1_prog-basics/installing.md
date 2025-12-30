# Getting going in your language



A few recommendations, if you want them. MATLAB has some special steps because we have a license through the school, though overall the installation process is probably the easiest. 

The other languages are open source, meaning you can follow any online tutorial to get them installed. Python technically can be installed with a graphical user interface (GUI), but I have grown to hate that environment -- I recommend miniconda, as described below. You will need to do a bit of work from the command line. Julia takes some command line work. C++ probably does, I'll be honest I have never installed it. If you flat-out do not want to do command line stuff, just go with MATLAB, but it makes me feel powerful to do command line stuff!


## MATLAB

MATLAB is the easiest to get going. As a CU student, you have free access if you create an account using your CU email address. Instructions are [here](https://oit.colorado.edu/software-hardware/software-catalog/matlab) -- use the ones for students, under "How to get it".

Once you have a MathWorks account and have it associated with the school's license, you can choose to download a desktop version of MATLAB, or to access the cloud version of the software. (See the note below about toolboxes before installing!) Students in previous semesters have used both options, so you can decide what works best for you. However, if you use the online version, you must download the code and upload it to your GitHub repository. I like the immediate access of having MATLAB installed on my machine, and I think it runs a bit faster, but you can access your code from any computer if you are using the online version.

The MathWorks site has many tutorials, maybe most notably the "MATLAB OnRamp". [You can find it here](https://matlab.mathworks.com/)... it is an "Online Training".


### Toolboxes

Basic MATLAB is going to be enough for the homework in this class, and you can always add toolboxes later. Some recommended ones:
- Simulink is used MCEN 4043: System Dynamics

Particularly if you are gearing up for MCEN 3047: Data Analysis and MCEN 4043: System Dynamics, I recommend installing: 
- Simulink
- The image processing toolbox (if you have any interest in that stuff)
- The machine learning toolbox
But you can always add packages later, as needed. Packages are immediately available in the online version if you ever need to just try something really quick.




## Python

There are multiple avenues here, and if you are confident enough to find you own way (e.g. with pip), I believe in you.

My recommendation is to [install miniconda](https://www.anaconda.com/docs/getting-started/miniconda/install) -- NOT the full Anaconda (which you can find nearby if you really want to, but I'm not linking it). Anaconda is attractive: it has everything you need in one install, but also a lot of unnecessary stuff. I grew to hate the navigator and "downgraded" to miniconda.

Miniconda will require you to install the packages you need, but it is lean because you are not going to install a bunch of useless stuff. Further, it is good code practice to establish separate environments for each of your projects with just the essentials for that project. Not really important for this class, but if you are curious we can talk or you can read about it.

Additionally, I am not fond of the IDEs (Integrated Development Environment) that come with Anaconda. I much prefer [VS Code](https://code.visualstudio.com), which even supports Jupyter Notebooks these days. You can technically incorporate VS Code into the Conda Navigator but my recommendation is: don't.

### Package management

Assuming you are using miniconda, [this page has instructions](https://www.anaconda.com/docs/getting-started/working-with-conda/packages/install-packages). Note that miniconda still uses "conda" in the command line. 
:::{aside}
pip is another option, really it's not that different. If you have reason to go that way, do it, plenty of tutorials around.
:::

:::{tip}
If you do want to create separate environments, e.g., one for your homework repository, one for the machine learning project, you can. From the command line, you would start with something like ```conda create --name homework``` and then ```conda activate homework``` puts you in that environment, and then ```conda install numpy``` would get you numpy in that environment. You need to install packages in each environment -- you might technically have numpy installed two or three times. But this is the way to manage conflicts: TensorFlow, for example, apparently doesn't play nice with numpy version 2.0 or higher... though I reverted back to that version of numpy and still couldn't get it to work!
:::



## Julia

Go [here](https://julialang.org), and the [recommended IDE](https://www.julia-vscode.org) is again VS Code, and there is again [a debugger](https://www.julia-vscode.org/docs/stable/userguide/debugging/).

Though Julia is technically a compiled language, working within VS Code makes it not feel compiled, which is nice.

## C++

You are on your own! You might talk to our TAs, they have experience with C++... I do not. If you took CSCI 1300 you are hopefully good to go.