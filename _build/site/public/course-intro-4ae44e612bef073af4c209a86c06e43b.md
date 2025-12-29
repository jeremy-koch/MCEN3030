# Introduction


:::{topic} Welcome to MCEN 3030: Computational Methods!
This course is offered by The University of Colorado Boulder Department of Mechanical Engineering, taught by Professor Jeremy Koch in the spring 2026 semester. We will learn about many of the mathematical algorithms that power engineering calculations. This is an exciting topic, as it allows us to study problems that go beyond what we can do with pencil and paper.
:::



## Scope

This is an introductory course with a large amount of coding, though it is arguably more of an "applied math" course than a programming course. Most of the heavy lifting will be done with ```for```, ```while```, ```if```, and thoughtful use of arrays. We will build our own versions of optimization algorithms, finite-element calculators, and differential equation solvers and that will allow us to better understand: what information is needed in these methods, what errors might we see, and what can we do if our approach is not working.







## Some policy highlights

- We will use the ["flipped classroom" model](flipped-classroom.md) and will cultivate a classroom environment that is highly collaborative.

- [You can choose what language you use](languages.md). MATLAB, Python, or Julia (ask me about others). AI will help you get your feet underneath you, and I have built [a page that includes pretty much all the commands](../1_fundamentals/coding-elements.md) you will need this semester, in those three languages. (Again, let's talk about other languages.)

- "AI will help you get your feet underneath you"? Yep, you have a [green light to use AI](AI.md) on the homework and project in this course. However, make sure to [use it responsibly](responsible-AI.md) -- the exams are pencil and paper only, no electronics.

## Some content highlights

- We will use GitHub Classroom. GitHub "repositories" are a very standard way to share code, and this organization might be one of the most important lessons of the semester.
- We will learn how to fit models, including nonlinear ones, to experimental data.
- We will do an introduction to machine learning, including a project.
- We will solve coupled nonlinear differential equations, including those that describe [mathematical chaos](https://en.wikipedia.org/wiki/Lorenz_system).







## How to use this site

I prepared this site to augment the learning that occurs elsewhere -- a rephrasing of the lecture (video) material that may clarify things, and a reference if you are quickly looking for an equation. It is not as detailed as a textbook and does not have many examples. 

It is a living document that will have things added and removed frequently. As such, I do NOT recommend forking this repository (if you know how to do this) -- if you are reading this early in the semester, there could be 50% more material by the end of the semester, I probably have incomplete pages floating around, and I might decide to eliminate some content in favor of adding other content.

- Course units are in the panel on the left, and clicking them will open a drop-down menu. Each item in that drop-down menu is a short reading. The readings are mostly about the motivation and the math, though sometimes code is included. Expect to read 1-3 of these before each class period (alongside watching the videos).
- Because this is a "{abbr}`polyglot (many languages)`" course, most of the times that code is referenced, it will be included in an environment like that below. You can choose the tab for your language, then see the code. In the top-right corner of each coding environment, you can choose an icon to copy that code block, and then you can paste it into your working environment and run it. Please confirm the code does what you think it does! Maybe I made a mistake!
- In the top-right corner of this site is a search bar. So, if you are looking for references to _Taylor Series_ within this site, you can search for it up there.
- At the end of each unit (the topics on the left) is a "Summary" page. These will include questions like "how would you do this?" This is your study guide for the exams! Exam questions will be about using the functions we write this semester -- you will need to create the inputs, understand and call the functions, and handle the outputs.
<!-- :::{caution}
Overuse of AI might keep you from understanding the inputs/outputs of the functions, and you might struggle with the auxiliary tasks, e.g.: creating an input array of evenly spaced numbers, preallocating space for the output array, defining a function. You need to figure out how to use AI responsibly. [I give recommendations here](responsible-AI.md).
::: -->

::::{tab-set}
:::{tab-item} MATLAB
```matlab
f=@(x,a) sin(x)+a;
```
:::
:::{tab-item} Python
```python
f=lambda x,a: np.sin(x)+a
```
:::


:::{tab-item} Julia
```
f=(x,a) -> sin(x)+a
```
:::


<!-- :::{tab-item} C++
??
::: -->
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