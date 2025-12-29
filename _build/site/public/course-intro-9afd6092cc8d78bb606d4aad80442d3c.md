<!-- # Introduction to Computational Methods -->


:::{topic} Welcome to MCEN 3030: Computational Methods!
This course is offered by The University of Colorado Boulder Department of Mechanical Engineering, taught by Professor Jeremy Koch in the spring 2026 semester. We will learn about many of the mathematical algorithms that power engineering calculations. This is an exciting topic, as it allows us to understand problems that go beyond what we can do with pencil and paper.
:::



## Scope

This is an introductory course with a fair amount of coding, though it is arguably more of an "applied math" course than a programming course. We aren't going to reinvent SolidWorks this semester, but we will learn about stiffness matrices and matrix inversion, which is ostensibly what is going on under the hood in SolidWorks. We also are not writing detailed software packages with fancy user interfaces -- it is going to be mostly just the math, implemented with basic programming ideas like array indexing, for loops, while loops, etc. The hope is that, by examining the fundamentals of these ideas, you will have some perspective on their utility and limitations. Further, you will be ready to tackle more detailed/complicated ideas if you decide to continue your studies of computational methods in advanced courses.

Our focus this semester is less about using the tools and more about understanding the tools. We will build our own versions of things like optimization algorithms and differential equation solvers and that will allow us to better understand: what information is needed, what errors might we see, and what can we do if our approach is not working.

<!-- :::{important}
More important than the individual topics 
::: -->








## Some policy highlights

- We will use the ["flipped classroom" model](flipped-classroom.md) and will cultivate a classroom environment that is highly collaborative.

- [You can choose what language you use](languages.md). MATLAB, Python, or Julia, maybe C++, and you can ask me about others. AI will help you get your feet underneath you, and I have built [a page that includes pretty much all the commands](../1_fundamentals/coding-elements.md) you will need this semester, in those four languages. (I can probably add more languages... I don't know C++ and was still able to put that together. But I really think those are the four best choices.)

- "AI will help you get your feet underneath you?" Yep, you have a [green light to use AI](AI.md) on the homework and project in this course. However, make sure to [use it responsibly](responsible-AI.md).

## Some content highlights

- We will spend the first day or two understanding GitHub. GitHub "repositories" are a very standard way to share code, and this will force us to think carefully about how to manage and organize files -- maybe one of the most important lessons of the semester.
- 
- We will learn the method of steepest ascent, which underlies many machine learning algorithsm.
- We will do a machine learning project. Broadly speaking, machine learning is about giving a computer a training data set, from which it methodically identifies patterns, and then uses that information to predict things about new data. A classic example is to give the program a picture and ask "is this an apple?" If it has been trained on a robust data set, it might get it right 90+% of the time.
- We will solve coupled nonlinear differential equations, including those that describe [mathematical chaos](https://en.wikipedia.org/wiki/Lorenz_system).







## How to use this site

I prepared this site to augment the learning that occurs elsewhere -- a rephrasing of the lecture (video) material, and a reference if you are quickly looking for an equation. It is not as detailed as a textbook and does not have many examples. 

It is a living document that will have things added and removed frequently. As such, I do NOT recommend forking this repository (if you know how to do this) -- if you are reading this early in the semester, there might be 50% more material by the end of the semester, and I might decide to eliminate some content in favor of adding other content.

- Course units are in the panel on the left, and clicking them will open a drop-down menu. Each item in that drop-down menu is a short reading. The readings are mostly about the motivation and the math, with some code is included.
- Because this is a "polyglot" course, most of the times that code is referenced, it will be included in an environment like that below. You can choose the tab for your language, then see the code. In the top-right corner of each coding environment, you can choose an icon to copy that code block, and then you can paste it into your working environment and run it. Please understand that it is a big undertaking to include this feature, and there may be some small mistakes in the code! Confirm it does what you think it does!
- In the top-right corner of this site is a search bar. So, if you are looking for references to "Taylor Series", you can search for it up there. It will return instances from within this site.
- At the end of each unit (the topics on the left) is a "Summary" page. These will include questions like "how would you do this?" This is your study guide for the exams! Exam questions will be about using the functions we write this semester, and part of that is writing the code that glues everything together. So you will need to create the inputs, understand and call the functions, and handle the outputs, and maybe there will be some problems where you need to interweave two functions!
:::{caution}
Overuse of AI might keep you from understanding the inputs/outputs of the functions, and you might struggle with the auxiliary tasks, e.g.: creating an input array of evenly spaced numbers, preallocating space for the output array, defining a function. You need to figure out how to use AI responsibly. [I give recommendations here](responsible-AI.md).
:::

::::{tab-set}
:::{tab-item} MATLAB
```matlab
f=@(x,a) sin(x)+a;
```
:::
:::{tab-item} python
```python
f=lambda x,a: np.sin(x)+a
```
:::


:::{tab-item} Julia
```
f=(x,a) -> sin(x)+a
```
:::


:::{tab-item} C++
??
:::
::::






## A brief comment

This webpage is hardly a book, more like a pamphlet, and it alone is not going to allow you to succeed in this course. We additionally have lecture videos, and more importantly, in-class work and homework that is going to go much further towards getting you to understand the content.

That being said, this webpage is hopefully going to be a resource for you, and you should read the relevant sections I point before class and reference this first when you have questions (use the search bar!). I estimate the total word count on all these pages to be about 30000... which sounds like a lot, but a textbook has about 300 words per page, so this is something like 100 pages. Over the course of our 15 weeks together, it is incredibly reasonable to ask you to read and digest this volume of information -- less than 10 pages per week!


Note that, in my [tips for success](../9_readings/success.md) page, I comment that:
- Your ability to focus is correlated with your career success. So: settle in and pay attention as you read for a few minutes.Develop that "muscle".
- AI is depriving students of their ability to focus and take in the details, instead providing quick and easy "summaries". Every page on this site is basically already summary, don't be summarizing a summary!
- Passivity is getting you nowhere. Think about the material after you read a section, get a pencil out and derive something yourself, get curious ("why doesn't this work?"), do some digging, connect the dots.

One of my big goals this semester is to empower students.



```{figure} forest_fire.png
:alt: 
:width: 300px
:align: center

A quick example of where you might take your wisdom after completing MCEN 3030. (Sorry, won't cover this in class!) [Agents.jl](https://juliadynamics.github.io/AgentsExampleZoo.jl/dev/examples/forest_fire/) is a Julia package that can implement flocking/swarming models -- really difficult to understand with pencil and paper, as there are often hundreds or thousands of entities interacting in these systems. One of their examples implements a forest fire model -- unfortunately very relevant to us in Colorado.
```