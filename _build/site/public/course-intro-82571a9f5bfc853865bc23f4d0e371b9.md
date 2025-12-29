# Intro

**Author:** Jeremy Koch

Welcome to MCEN 3030: Computational Methods



## Some policy highlights

- We will use the ["flipped classroom" model](flipped-classroom.md) and will cultivate a classroom environment that is highly collaborative.

- You have a [green light to use AI](AI.md) in many course aspects. However, a strong warning: the exams in this course make up most of the grade, and they are pencil and paper with no electronics.

- [You can choose what language you use](languages.md). MATLAB, Python, Julia, and C++ are good, and you can ask me about others. AI will help you get your feet underneath you!


## Some content highlights

- We will spend the first week setting up GitHub. GitHub "repositories" are a very standard way to share code, and this will force us to think carefully about how to manage and organize files -- maybe one of the most important lessons of the semester.
- We will do a machine learning project. Broadly speaking, machine learning is about giving a computer a training data set, from which it methodically identifies patterns, and then uses that information to predict things about new data. A classic example is to give the program a picture and ask "is this an apple?" If it has been trained on a robust data set, it might get it right 90+% of the time.
- We will solve coupled nonlinear differential equations, including those that describe [mathematical chaos](https://en.wikipedia.org/wiki/Lorenz_system).







## How to use this site

- Course units are in the panel on the left, and clicking them will open a drop-down menu. Each item in that drop-down menu is a short reading on the topic, to augment the course videos. The readings are mostly about the motivation and the math, though some code is included.
- Because this is a "polyglot" course, most of the times that code is referenced, it will be included in an environment like that below. You can choose the tab for your language, then see the code. In the top-right corner of each coding environment, you can choose an icon to copy that code block. While we can't run the code on the webpage, you can paste it into your working environment and run it. Please understand that it is a big undertaking to include this feature, and there may be some small mistakes in the code! Confirm it does what you think it does!
- In the top-right corner of all pages is a search bar. So, if you are looking for references to "Taylor Series", you can search for it up there.
- At the end of each unit (the topics on the left) is a "Summary" page. These will include questions like "how would you do this?" This is your study guide for the exams! Exam questions will be about using the functions we write this semester, and part of that is writing the code that glues everything together. So you will need to create the inputs, understand and call the functions, and handle the outputs, and maybe there will be some problems where you need to interweave two functions!
:::{warning}
Overuse of AI might keep you from understanding the inputs/outputs of the functions, and you might struggle with the auxiliary tasks (e.g. creating an input array of evenly spaced numbers, preallocating space for the output array) too. You need to figure out how to use AI responsibly. [I give recommendations here](responsible-AI.md).
:::

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






### A brief comment

This webpage is hardly a book, more like a pamphlet. I estimate the word count as ____, which is something like ____ pages. Over the course of our 15 weeks together, it is incredibly reasonable to ask you to read and digest this volume of information. Your first action, should you have a question about course content, is to reference this webpage.

Note that, in my [tips for success](../9_readings/success.md) page, I comment that:
- Your ability to focus is correlated with your career success. (So: settle in and read for a few minutes, develop that "muscle".)
- AI is depriving students of their ability to focus and take in the details. (So: go against the trend... and settle in and read for a few minutes.)
- That passivity is getting you nowhere. (So: do some digging to answer your questions, don't just email me)