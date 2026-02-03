# Notebook files

As (more-or-less) scripting languages, MATLAB/Python/Julia code can be implemented via notebooks. The three big benefits of notebooks are, in my view:
1. You run snippets of your code piece-by-piece, which is useful if there is some human intervention at some point within your code (or if you are developing and just want to make sure an early step is looking OK). For example, if you are trying to measure the position of something in a series of images, you will likely use an edge-detection algorithm. Within your notebook, check one frame early to make sure the threshold is good, tweak if necessary, and then move on with the full processing.
2. Code outputs, including figures/images, are part of the notebook. No hopping between windows or your code and the terminal to see the outputs -- it's right there embedded within the notebook.
3. Code can be interspersed with more readable text in the markdown language. If, for example, you'd like to provide instructions on how to change said threshold, or want to display a nicer model-fit equation (like this: $y=a_0 + a_1 x + a_3x^3$ instead of this: ```y=a_0 + a_1*x + a_3*x**3```), you can do that.

The tool for each of the languages is different -- I'll provide an overview below, and you can always search around on the internet for tips/troubleshooting!

## MATLAB

MATLAB has "MATLAB Live Scripts" with extension ```*.mlx```. You can create a new one from New -> Live Script. Within the "Live Editor" you should see "Text" and "Code" buttons at the top -- text is where you explain what your code is doing, code is... code. A bit to the right you'll see "Run Section", etc., which is where you can break your code up into sections and run them individually.

The document itself has code/text in a column and outputs in another column. If you end up with several plots, it can be a bit buggy, but I think MathWorks has improved in recent versions.

:::{seealso}
[MATLAB's documentation](https://www.mathworks.com/help/matlab/matlab_prog/what-is-a-live-script-or-function.html)
:::

## Python

Python has the most options for notebooks/notebook interfaces, I encourage you to explore.

The big one is "Jupyter Notebook" with extension ```*.ipynb``` (after "interactive Python Notebook). You can install it as a package via conda.

I have, until recently, launched Jupyter from the command line, and it creates a tab in your default web browser (though it is still local). For me, scrolling was a bit buggy, and I switched to opening in VS Code. [Instructions here](https://code.visualstudio.com/docs/datascience/jupyter-notebooks).

:::{seealso}
There are other notebook tools out there, e.g. [Marimo Notebooks](https://towardsdatascience.com/why-im-making-the-switch-to-marimo-notebooks/). (Disclosure, I have not tried this yet.)
:::

## Julia

You can use Jupyter Notebooks in Julia, but most seem to prefer [Pluto Notebooks](https://plutojl.org). I haven't gotten a chance to try these yet! Maybe in the few minutes I have left before class...