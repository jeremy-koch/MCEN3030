# Intro

**Author:** Jeremy Koch

Welcome to MCEN 3030: Computational Methods



## Some policy highlights

- We will use the ["flipped classroom" model](flipped-classroom.md).

- As part of this, we will cultivate a classroom environment that is highly collaborative.

- You have a green light to use AI in many course aspects. However, a strong warning: the exams in this course make up most of the grade, and they are pencil and paper with no electronics.
:::{aside}
AI = artificial intelligence

LLM = large language model
:::


- You can choose what language you use (perhaps with some limits). If you really enjoy C++, you can use it. If you want to go with a language you will (probably) see in MCEN 3047: Data Analysis and MCEN 4043: System Dynamics, think about MATLAB. If you are a bit adventurous, try this new language called Julia. AI will help you get your feet underneath you!


## Some content highlights

- We will spend the first week setting up GitHub. GitHub "repositories" are a very standard way to share code, and this will force us to think carefully about how to manage and organize files -- maybe one of the most important lessons of the semester.

- We will do a machine learning project

- We will solve coupled nonlinear differential equations, including those that describe [mathematical chaos](https://en.wikipedia.org/wiki/Lorenz_system)







## How to use this site

- Course units are in the panel on the left, and clicking them will open a drop-down menu. Each item in that drop-down menu is a short reading on the topic, to augment the course videos.


- Because this is a "polyglot" course,
:::{aside}
"polyglot" = many languages
:::
most of the times that code is referenced, it will be included in an environment like that below: choose your language, then see the code in that language. In the top-right corner of each coding environment, you can choose an icon to copy that code block. While we can't run the code on the webpage, you can paste it into your working environment and run it. Please understand that it is a big undertaking to include this feature, and there may be some small mistakes in the code! Confirm it does what you think it does!
::::{tab-set}
:::{tab-item} MATLAB
```matlab
f=@(x) sin(x);
```
:::
:::{tab-item} python
'''python
f=lambda x: np.sin(x)
'''
:::


:::{tab-item} Julia

:::


:::{tab-item} C++

:::
::::


- At the end of each unit (the topics on the left) is a "Summary" page. These will include questions like "how would you do this?" This is your study guide for the exams! Exam questions will be about using the functions we write this semester, and part of that is writing the code that glues everything together. So you will need to create the inputs, understand and call the functions, and handle the outputs, and maybe there will be some problems where you need to interweave two functions!
:::{warning}
Overuse of AI might keep you from understanding the inputs/outputs of the functions, and you might struggle with the auxiliary tasks (e.g. creating an input array of evenly spaced numbers, preallocating space for the output array) too. You need to figure out how to use AI responsibly. [I give recommendations here](responsible-AI.md).
:::

- In the top-right corner of all pages is a search bar. So, if you are looking for references to "Taylor Series", you can search for it up there.

### A brief, related comment

This webpage is hardly a book, more like a pamphlet. I estimate the word count as ____, which is something like ____ pages. Over the course of our 15 weeks together, it is incredibly reasonable to ask you to read and digest this volume of information. Your first action, should you have a question about course content, is to reference this webpage.

Note that, in my tips for success page, I comment that:
- Your ability to focus is correlated with your career success. (So: settle in and read for a few minutes.)
- AI is depriving students of their ability to focus. (So: go against the trend... and settle in and read for a few minutes.)
- That passivity is getting you nowhere. (So: do some digging to answer your questions, don't just email me)