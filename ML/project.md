# Machine Learning Project


:::{tip}
You will complete this project in our GitHub Classroom, which by default means your repository is private. However, if you are proud of your work, and have done a good job preparing your report, this may be something that you publish publically (easy to copy the repository) and list on your personal webpage or resume. Not required, but maybe that is motivation!

However, note that we are using AI assistance here. The message, therefore, is probably not "look at what I coded!" but is more "look at my engineering wisdom and how I used this tool to evaluate it".
:::






## Project topics




1. 
2.
3.



### Extra credit opportunity

You may propose and complete a second machine learning project. The first required one is worth 5% of your overall grade, the second is worth 1% bonus for the same requirements, more work because you have to propose the topic. If you complete a third project, it is worth 0.000000000000000000000001% bonus and my [round-off error](../2_foundations/error.md) in the overall grade calculation kicks in at 4 or 5 digits.



## Rules

1. You cannot upload your data set to an AI tool. If you use an LLM, you must describe the problem and data to the LLM in your own words and then implement the code on your own computer. However, you can ask the LLM to include code that produces a summary of the performance and can copy and paste that in, to work iteratively. An example of a summary would be something like a success rate on your validation test. (It seems like these are typically included by the LLM without asking.)
2. You should not use basic regression on any of these projects (and I don't think that is the best tool, anyway). The purpose is to get you exposure to other techniques -- random forest, classification, etc.


## LLM use

You are allowed and encouraged to use LLMs in this project, with the caveat that you must document those interactions (details below). FYI, I am working on a machine learning project for the department, and the most recent version of the code is about 2000 lines. I, a human, wrote about 100 of them.
:::{aside}
My opinion about LLMs in general is that they are plagiarism machines, but I feel better about using them for code. I suspect they have digested [the extensive, detailed documentation](https://github.com/scipy/scipy) of these functions and have been programmed to stitch together inputs and outputs to achieve tasks.
:::

As of writing this, I do not pay for any LLM. My understanding is that folks with a colorado.edu email address now have free access to [Google Gemini](https://gemini.google.com/) and [ChatGPT edu](https://chatgpt.com) (I have only used the former). I have also experimented with the free version of [Claude](https://claude.ai/). I have not tried [Microsoft Copilot](https://copilot.microsoft.com). There are others out there -- I won't limit you.

At various points, I ask you to 




:::{warning}
If you stick with free versions, it will be fine, but there are ~daily limits. Don't expect to get it all done in one session, you might need to come back the next day. 
:::

:::{dropdown} If you do not want to use an LLM...
:open:
If you are averse to using an LLM, let's talk. We can find 
:::

## Step 1: Choose your problem and do some preliminary thinking (no coding)


::::{tab-set}
:::{tab-item} Problem 1

:::


:::{tab-item} Problem 2
:::


:::{tab-item} Problem 3

:::
::::

Examine the data set (manually) and find a case that validates your assumptions.


## Step 2: Plan a path forward with an LLM

Your interaction should look something like this.
1. Describe the problem, including the data set and the question you'd like to ask. Don't press enter yet -- include another sentence like "I would like to approach this as a machine learning problem, can you recommend a strategy?" Don't press enter yet -- end the prompt with something like "Let's talk ideas first and I'll ask for the code later."
2. The LLM will likely suggest a pathway that is relevant to the problem -- "Random Forest" or "". It might ask a follow-up question like "how big is your data set?" Hopefully it will give a good explanation, and you can ask follow-up questions. In your report, you will need to explain why you chose your path -- this is your opportunity to get some information.
3. Once you feel OK about the background, go ahead and ask for the code. Be specific: "OK, generate the python code" (though the LLMs learn your preferences over time). You can use code files -- .m, .py, .jl, -- or [notebook files](../1_prog-basics/notebooks.md) -- .mlx, .ipynb, and Pluto uses .jl again I think. If you prefer one over the other, work with it: "can you describe cell-by-cell how this could be implemented in a python notebook?"








## Step 3: Implement the code



## Tips

- Sometimes the LLM will say "replace section 4 of the code with this". Try to work with it, but if it is getting confusing you can always say "give me a summary of all the current code".
- 