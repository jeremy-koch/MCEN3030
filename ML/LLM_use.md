# LLM use in Machine Learning

You are allowed and encouraged to use {abbr}`LLMs (large language models)` on this project. FYI, I am working on a machine learning project for the department, and the most recent version of the code is about 2000 lines. I, a human, wrote less than 100 of them. We are going to let LLMs do the heavy lifting on the coding side while we focus on interpreting the results and applying our engineering intuition.
:::{aside}
My opinion about LLMs in general is that they are plagiarism machines, but I feel better about using them for code. I suspect they have digested [the extensive, detailed documentation](https://github.com/scipy/scipy) of these functions and have been programmed to stitch together inputs and outputs to achieve tasks. You can form your own opinion, or not let it bother you either way!
:::



As of writing this, I do not pay for a subscription to any LLM. My understanding is that folks with a colorado.edu email address have free access to [Google Gemini](https://gemini.google.com/) and this is what I have been using (partially because Gemini claims to not be training based on our conversations, and partially because the limits are higher than free versions of other LLMs because of our school's agreement). The school recently announced a partnership with [ChatGPT](https://chatgpt.com), which may not be active yet (but of course ChatGPT is available, and I use it sometimes). I have also experimented with the free version of [Claude](https://claude.ai/) and really like it. I have not tried [Microsoft Copilot](https://copilot.microsoft.com). There are others out there -- I won't limit you.

:::{warning}
If you stick with free versions, it will be fine, but there are usage limits. Don't expect to get it all done in one session, you might need to come back in a few hours or the next day.
:::



## A good first prompt

Effective prompting provides context and asks for specifics. Starting with "I want to do a machine learning project" will be inefficient -- it is going to ask you incremental questions, maybe take you down the wrong path for a while, and waste a lot of time. Instead, be thoughtful in your creation of a detailed first prompt. Don't be scared of writing a paragraph or even two, it can handle it.

Here is more-or-less what I would use in this project:
> *I would like to do a machine learning project where the goal is to predict whether a fruit is an apple, peach, nectarine, plum, or kiwi based physical measurements. I have a spreadsheet with columns 'fruit', 'weight', 'avg_radius', 'eccentricity', and 'hardness_value'. There are approximately 4000 rows. I will ask for Python scikit-learn code soon, but first: Can we talk about the best way to model this data set?*

Notice:
- I said I wanted to do machine learning.
- I said the goal and a little background.
- I described the data set. You are prohibited from uploading your data to an LLM and having it work for you, but trust me, giving it the labels like this is going to be enough.
- It is usually a good idea to mention the size of the data set, as that might factor-in to the approach decision.
- I specified my programming language. (The LLMs will learn about you though and know that, e.g., you use Python.)
- I strongly recommend asking it NOT to code at first. Instead, ask it to clarify details and explain what approach it recommends. It will save you time and will help you understand what is going on.


## The initial follow-up prompts

You can ask clarifying questions. E.g.: Why random forest, why not neural nets? What is a random forest? What is a neural net? 

Once it gives you code and you run it, it will probably throw some sort of error. The file is named differently (hopefully you can debug that one!), it finds a {abbr}`NaN (not a number)` in the data set, etc. You can copy and paste those messages from your terminal/command window, but make sure you are grabbing the relevant bit: there are usually several lines in the error message, about how it couldn't do this because it couldn't do that because it couldn't do this. Determine which part of the "traceback" is relevant, and send that over to the LLM. 

It will take just a few minutes to get all the errors smoothed-out, and before you know it you'll have some results.

## Iterating on the model

It should produce some plain-text results in your terminal/command window, basically a summary of the validation step. The results will never be perfect, and maybe you will never be able to reasonably get above 80%. That is just what the data says -- real life is messy and noisy. 
:::{important}
It is important to acknowledge the limitations of your work so that your co-workers/clients understand the risks!
:::

You can paste the plain-text results (shouldn't be more than 10 lines) back into the LLM to initiate a discussion on how to iterate to improve upon the predictions. Maybe you need to adjust some of the [hyperparameters](https://en.wikipedia.org/wiki/Hyperparameter_(machine_learning)) like the maximum depth or maximum number of features per tree. You'll talk about this in your report.


:::{note} Recall...
We talked about [overfitting](../5_fitting/meaningR2.md). In machine learning, they sometimes talk about "memorizing the data set". It can be that you adjust hyperparameters until the model is just memorizing!
:::