# Responsible use of AI

<!-- **Author:** Jeremy Koch -->

## Introduction

In this course, you more-or-less have the green light to use AI on homework (not on exams or in-class problems, which are pencil and paper). Here, I will give a perspective on AI misuse and also will give recommendations on how it can be properly used.

:::{warning}
If the instructional staff is not policing AI use, it is you, the student, who must judge proper use. Think about the following: understanding an answer is very different from being able to produce an answer. I suspect many students are asking LLMs for a solution, then they "study" it, and then think they "understand" the problem. This is almost never true.
<!-- The purpose of homework is not to finish it as quickly as possible. You should spend however long it takes to actually understand the problems! -->
:::


## AI Misuse

Your instructors are aware that AI use is widespread among students. It is misuse that we are concerned about -- specifically, we worry that students are not actually developing as engineers because they 



An example of audacious behavior: I have seen is students taking screenshots of problems, pasting into ChatGPT, and then copying the results. These students possibly did not even read the problem! 
:::{tip}
I have given the following (controversial) advice in the past, and I guess will give it here: If you care so little about the content of mechanical engineering that you are copying answers straight from the LLMs, maybe you would be more interested in a different major?
:::



If you are interested, you can read about [Bloom's Taxonomy](https://en.wikipedia.org/wiki/Bloom%27s_taxonomy), which is a framework for understanding how students master a topic. Studying LLM solutions may help you with "knowledge" and "comprehension", the lower levels of the taxonomy. ("Ah that is how to format the inputs".) It will not help you get better at the "application", "analysis", "synthesis", or "evaluation" levels, and those are the actually interesting parts of engineering that you are hopefully excited to do.



## AI Reasonable Use

<!-- It is my assessment that, overall, LLMs are plagiarism machines. It's just that they go word-by-word, statistically, and so it is difficult to point to a single source from which their text was plagiarized. However, when it comes to coding, I have a comforting hypothesis that the LLMs are looking at code documentation (e.g. for [numpy piecewise](https://numpy.org/devdocs/reference/generated/numpy.piecewise.html)) and logicking together the inputs and outputs to achieve a goal. I feel a bit better about that, at least from an ethical standpoint. -->

This does not mean that LLMs are there to help you learn: if you want to learn, you must be thoughtful about how you interact with them. I cannot make you be thoughtful. In particular: you must resist the urge to jump to the answer. So here are my recommendations on how to responsibly use AI, if your goal is to actually learn:
- Do not go to AI at the beginning. Do not go to AI immediately when you get stuck. Getting stuck and thinking about how to get unstuck is very much an authentic engineering experience and is probably the best way to learn. Reread the problem, think about what information is given, what information is missing that is needed, what assumptions could be made etc. A secret: I care more about the first 5 minutes of you working on the homework problem, when you are confused but figuring it out, than the remaining 55 minutes of you grinding through calculus and algebra. The unfortunate thing is that I can't actually assess that first five minutes, but I can for sure assess whether you report 56.1 m/s.
- If, after a while of being stuck, you have not made much progress, then talk to an AI. But write it in your own words, and try to be specific about the issue. "I am trying to write a root-solving algorithm using Newton-Raphson Method. I am stuck trying to figure out when to end the iterations. I suspect I should use a while statement but am confused on how to implement the logic." Honestly, I don't think the AI will need all that detail, but this is not about what the AI needs, it is about what you need! You need to get practice with using engineering language to define problems!
- If you encounter a cryptic error message, again: try to decipher it on your own, and if you can't figure it out, ask and be specific. Programming languages/environments are usually decent at explaining where the error occurs, giving a line number and the error type (ValueError, KeyError, etc.). "I get the following error: \<whatever the error is\>. It seems to be related to my function inputs but I am not sure what the message means." That is not unreasonable, and again, you put some thought into it instead of just asking it to bail you out.
- Debugging via AI is a valid use, though I believe developing an eye for debugging is a very valuable skill. Try for a minute to debug on your own, but I get it: AI might save us from spending 90 minutes hunting for some tiny thing.
:::{tip}
If you would be ashamed to show your instructor your prompts, you are probably misusing AI.
:::


:::{warning}
The inputs to LLMs become part of its training data and thus that information essentially becomes public. You may be in a situation where your organization has an agreement with a particular LLM to not use the data for training, but I would in general be very careful about what you share. Indeed, in your job, you may be prohibited from sharing proprietary information like diagrams, performance metrics, or computer code with LLMs. You need to practice talking about the big ideas and then implementing the specifics locally, without giving away company secrets to LLMs!
:::
:::{aside}
CU seems to have an agreement with Google Gemini where our chats do not go to training their models. (I am not sure if students have the same access as faculty?)
:::