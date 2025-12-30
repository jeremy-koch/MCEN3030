# Responsible use of AI

<!-- **Author:** Jeremy Koch -->

## Introduction

In this course, you have the green light to use {abbr}`AI (artificial intelligence)`/{abbr}`LLMs (large language models)` on homework (though not on exams or in-class problems, which are pencil and paper). Here, I will give a perspective on AI use and misuse, including recommendations on how it can be properly used by students.

Something to think about: understanding an answer is very different from being able to produce an answer. I am worried many students are asking LLMs to produce a solution, then they "study" it, and then think they "understand" the problem. This is never true -- you cannot learn to solve problems unless you, yourself, face the decisions and uncertainty. There is no uncertainty when you are handed a solution.

:::{attention}
A moment of blunt honesty: Misuse of AI is THE reason why homework is weighted relatively low in the final grade calculation in this class (and likely will be low in all of my classes going forward). I would strongly prefer a teaching environment where final grades were not so dependent on performance during three time-limited exams -- I do not believe that working quickly makes one a good engineer, at all. However, I also do not want to have a class where a hard-working but imperfect student receives a lower grade than a student who puts in nearly zero effort.

The department might be going back to the old model of engineering education, where homework is not worth many points. But it is certainly worth doing to prepare for exams!
:::

At the same time...

:::{tip}
Green-lighting AI in this course opens up opportunities -- I am not TOO worried about allowing students to pick their programming language, I am looking forward to the machine learning project, and (I hope) students will get some experience in proper AI use.
:::


If the instructional staff is not policing AI use, it is you, the student, who must judge proper use.

## AI Misuse

We instructors worry that students are not developing as engineers because they are allowing the hard (but meaningful) work to be done by LLMs. A particularly audacious behavior that I have observed several times: students taking screenshots of problems, pasting into an AI, and then copying the results. These students possibly did not even read the problem!
:::{tip}
I have the following (controversial) advice: If these students care so little about the content of mechanical engineering that they are copying answers straight from the LLMs, maybe they would be happier in a different major? They are certainly smart enough to be mechanical engineers, but are they interested?
:::

But milder uses are also sometimes problematic. Many students claim they use AI "just to get started" or "just when stuck". Getting started on problems and getting unstuck is like 95% of the learning that occurs on the homework! I actually care very little that you do all the algebra correctly once you see the path forward -- finding the path forward is the hard part. As mentioned above: understanding an answer is very different from being able to produce an answer.

If you are interested, you can read about [Bloom's Taxonomy](https://en.wikipedia.org/wiki/Bloom%27s_taxonomy), which is a framework for understanding how students master a topic. Studying LLM solutions may help you with "knowledge" and "comprehension", the lower levels of the taxonomy. ("Ah that is how to format the inputs" -- that is indeed a good, useful lesson.) It will not help you get better at the "application", "analysis", "synthesis", or "evaluation" levels, and those are the actually interesting parts of engineering that you are hopefully excited to do.



## AI Reasonable Use

<!-- It is my assessment that, overall, LLMs are plagiarism machines. It's just that they go word-by-word, statistically, and so it is difficult to point to a single source from which their text was plagiarized. However, when it comes to coding, I have a comforting hypothesis that the LLMs are looking at code documentation (e.g. for [numpy piecewise](https://numpy.org/devdocs/reference/generated/numpy.piecewise.html)) and logicking together the inputs and outputs to achieve a goal. I feel a bit better about that, at least from an ethical standpoint. -->

If you want to learn while using an LLM, you must be thoughtful about how you interact with them. I cannot make you be thoughtful -- you must resist the urge to jump to the answer. So here are my recommendations on how to responsibly use AI, if your goal is to actually learn:
- Do not go to AI at the beginning. Do not go to AI immediately when you get stuck. Getting stuck and thinking about how to get unstuck is very much an authentic engineering experience and is probably the best way to learn. Reread the problem, think about what information is given, what information is missing that is needed, what assumptions could be made etc. A secret: I care more about the first 5 minutes of you working on the homework problem, when you are confused but figuring it out, than the remaining 55 minutes of you grinding through calculus and algebra. The unfortunate thing is that I can't actually assess that first five minutes, but I can for sure assess whether you do all the algebra right.
- If, after a while of being stuck, you have not made much progress, then talk to an AI. But write it in your own words, and try to be specific about the issue. "I am trying to write a root-solving algorithm using Newton-Raphson Method. I am stuck trying to figure out when to end the iterations. I suspect I should use a while statement but am confused on how to implement the logic." Honestly, I don't think the AI will need all that detail, but this is not about what the AI needs, it is about what you need! You need to get practice with using engineering language to define problems! (This is part of the reason we will have a lot of peer discussion in our [flipped classroom](flipped-classroom.md).)
- If you find yourself prompting incrementally, asking the AI to help with every step, pause. Review your notes, review the steps you've taken so far, and try to at least speculate about what is next. If you are being given every step, you probably are not learning!
- When you get towards the end, you might encounter a cryptic error message, again: try to decipher it on your own, and if you can't figure it out, ask and be specific. Programming languages/environments are usually decent at explaining where the error occurs, giving a line number and the error type (ValueError, KeyError, etc.). "I get the following error: \<whatever the error is\>. It seems to be related to my function inputs but I am not sure what the message means." That is not unreasonable, and again, you put some thought into it instead of just asking it to bail you out.
- Debugging via AI is a valid use, though I believe developing an eye for debugging is a very valuable skill. Try for a minute to debug on your own, but I get it: AI might save us from spending 90 minutes hunting for some tiny thing.
- Whenever you are "done", don't be done. Interpret the result yourself, decide if it makes sense, think about the steps it took to get there and the decisions that you needed to make along the way.

:::{tip}
If you would be ashamed to show your instructor your prompts, you are probably misusing AI.
:::

:::{warning}
The inputs to LLMs become part of its training data and thus that information essentially becomes public. You may be in a situation where your organization has an agreement with a particular LLM company to not use the data for training, but I would in general be very careful about what you share. Indeed, in your job, you may be prohibited from sharing proprietary information like diagrams, performance metrics, or computer code with LLMs. You need to practice talking about the big ideas and then implementing the specifics locally, without giving away company secrets to LLMs!
:::
:::{aside}
CU seems to have an agreement with Google Gemini where our chats do not go to training their models. (I am not sure if students have the same access as faculty?)
:::