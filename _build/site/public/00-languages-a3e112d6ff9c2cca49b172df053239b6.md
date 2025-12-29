# Languages

**Author:** Jeremy Koch<sup>1,2</sup> \

::::{tab-set}
:::{tab-item} MATLAB
Reasons to choose MATLAB:
- For students it is free.
- No package management: you can either download MATLAB (for )
- MATLAB has an excellent built-in debug mode.
- MATLAB has traditionally been used in MCEN 3047: Data Analysis and MCEN 4043: System Dynamics.
- It is a language for scientists and engineers. Matrix math is just: ```A*x```.
- Indexing starts with 1.

Reasons to NOT choose MATLAB:
- While it is 100% free for students, it is not free in the real world: a yearly license for an individual costs $1015.
- Related: some companies do use MATLAB and surely are getting a discount from that per-person price tag, but most companies are not going to want to pay thousands of dollars when there are many free options that can do all the same tasks.
- MATLAB allows you to be "sloppy" in ways that make serious programmers shake their head. It is VERY easy to accidentally redefine a 1xN array into a single scalar value, and MATLAB's flexibility will often let you do math with it still without error or warning. 
:::


:::{tab-item} python

Reasons to choose Python:
- For everyone it is free (open source).
- I find Python code to be clean and intuitive in comparison to MATLAB. Indenting/whitespace is used instead of end statements. (However, see the note below about numpy.)
- By a wide margin, data science people are using Python. I can't comment on whether it is actually better-suited for data science, but there is just more packages, more tutorials, more users to help you.



Reasons to NOT choose Python:
- Indexing starts with 0, which might annoy you enough to look elsewhere.
- There are plenty of tutorials available, but you must install .
- Base Python was not invented for engineers. NumPy/SciPy/Matplotlib have been thoroughly developed, but it just less appealing to have to deal with ```np.sin(x)``` instead of just ```sin(x)```. (Yes, I know you can ```from numpy import sin``` and then just use ```sin(x)``` but that is not all that would need importing... I think we'd at least need to import ```array``` as well. We usually just ```import numpy``` in its entirety.)
:::


:::{tab-item} Julia
Reasons to choose Julia:
- For everyone it is free (open source).
- It is a language developed for scientists and engineers.
- It allows the use of unicode characters. Thus, if you want to write an equation that has an $α$ in it, you can use ```α```. (In other languages we'd probably use ```a``` or ```alpha```, just not as satisfying.)
- Indexing starts with 1.

Reasons to NOT choose Julia:
- Julia is a compiled language. This means the first time you run it, it may be slow. If you are the type to make an incremental change, then run it to check the results, you may be frustrated by the slowness. It may still be fast enough to not bother you.
- It is the least well-developed of the languages in this list, meaning there are fewer tutorials, fewer third-party programs, and fewer users to help.
- It is not clear if Julia will continue to grow or if it will fade away.
- We will likely not have need to use the truly powerful aspects of Julia, e.g. multiple dispatch.
:::


:::{tab-item} C++
Reasons to choose C++:
- For everyone it is free (open source).
- You may have taken CSCI 1300, which uses C++, and want to continue with that.
- It has arguably been the language of "serious engineers" for the past 30 years. Robotics has a strong preference towards C++, and the biggest open-source computational fluid dynamics (CFD) code is https://www.openfoam.com, which is based in C++.

Reasons to NOT choose C++:
- C++ is a compiled language. This means the first time you run it, it may be slow. If you are the type to make an incremental change, then run it to check the results, you may be frustrated by the slowness. It may still be fast enough to not bother you.
- I think it is the ugliest and least-readable language of the four in the list. 
:::

::::

## Other languages

Contact me. Don't do assembly, machine learning, or FORTRAN (shudders).



## More reading

https://tobydriscoll.net/post/matlab-vs.-julia-vs.-python/