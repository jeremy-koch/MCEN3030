# Some thoughts on AI

**Author:** Jeremy Koch

## Motivation

Optional reading, if you care to hear my opinions. On the technical aspects of how LLMs work, I am far from an expert. But when it comes to AI use in engineering education, including how that manifests in your early career, I have done a lot of thinking on this issue.

## What are LLMs doing?

First, a bit of vocabulary.
- AI = artificial intelligence. This is a very broad idea that we, as a society, [have been thinking about for a long time](https://thejetsons.fandom.com/wiki/Rosey).
- LLM = large language model. This was the recent breakthrough. Trained on massive amounts of text, they are "predictive" in the sense that, given a bit of text, they can guess what bit of text comes next based on their training. 
:::{aside}
There is debate about whether LLMs represent a form of artificial intelligence, or are they simply statistics calculators. I lean more towards the latter.
:::
- Token == the calculation unit of LLMs. It is not quite a word.

So, a dismissive view of LLMs is that they are plagiarism machines, but maybe the blandest kind: they don't steal from one author, they have a knowledge base that includes 50 authors who have written a similar bit of text. If 13 of them followed up that bit of text with with a similar idea, and the other 37 had unique ideas, it is ostensibly going to follow-up with some average of the 13 ideas. After all, that is the one that is statistically most likely, and therefore "correct"?!

Let me emphasize again that I am not an expert on the technical side. I think a lot of the current research towards new models is about systematically examining the 37 other opinions, maybe in slightly different contexts, in order to judge if they should influence the output. When an LLM claims "PhD-level knowledge", it is likely trying to cut through the large amounts of less-expert knowledge to find the one or two pieces of genuine-expert knowledge, and that is a tougher problem.

## Some readings

The Atlantic has produced a steady stream of thought-provoking articles on AI use. Here are a few -- I don't endorse the views in any of them, but they might help you to shape your opinions.

- [The Entry-Level Hiring Process Is Breaking Down](https://www.theatlantic.com/ideas/2025/12/grade-inflation-ai-hiring/685157/).
> "In the past, companies looking for fresh entry-level talent could rely on a college graduate’s GPA as a mark of their intelligence and work ethic. Hiring managers could assess a candidate’s cover letter and interview performance to get a sense of their writing and communication skills. Now those signals have lost much of their value. Rampant grade inflation has rendered GPAs almost meaningless. The widespread use of AI to write cover letters—and even to assist with job-interview performance—has robbed those assessments of their predictive power."

- [The Age of De-Skilling](https://www.theatlantic.com/ideas/archive/2025/10/ai-deskilling-automation-technology/684669/).
> "

- [My Students Use AI. So What?](https://www.theatlantic.com/ideas/archive/2025/10/ai-college-crisis-overblown/684642/)

<!-- :::{aside}
https://en.wikipedia.org/wiki/Magnetic-core_memory
::: -->


<!-- ::::{tab-set}
:::{tab-item} MATLAB
```MATLAB
f=@(x) x^2
```
:::
:::{tab-item} python
```python
f=lambda x: x**2
```
:::
:::{tab-item} julia
```julia
f=lambda x: x**2
```
:::

:::: -->



# AI in Computational Methods

**Author:** Jeremy Koch

I could write many thousands of words on why AI is not good thing for students. Most notably: Who is going to hire an engineer who has outsourced all their thinking to AI? If I was looking to hire someone, I wouldn't care that a lot of relevant information is readily available on ChatGPT, I am looking for someone who is comfortable with engineering, who can see the connections, who can troubleshoot problems, and who I'd feel excited to work with. "Hold on, let me see what ChatGPT says"... I can ask ChatGPT too, thanks for your time but I think we are going to hire someone else.

An engineer who is solid at the fundamentals can use AI to supercharge their abilities, but overuse of AI is preventing many students from becoming solid at the fundamentals.

A class like MCEN 3030: Computational Methods is particularly vulnerable to AI misuse. As an example, the Newton-Raphson Method for determining the roots of a function has been known since the 1600's. I don't know .

This means that LLMs (large-language models) have for sure seen countless versions of the code on the internet, and so a simple prompt like "Write me python code that implements 1D Newton-Raphson" is going to give you a perfect implementation of the method. 


known to engineersIt was probably one of the first things to appear on the internet. 

## Course design

As I thought about designing the course, a few things were on my mind.
- I could officially prohibit AI. This would involve a lot of police-work on my end, which I have no appetite for, and it would likely lead to an adversarial relationship between me and you. I for sure don't want that. 
- I am uncomfortable with the fact that a student who has misused AI may receive a higher grade than an earnest student who made a few mistakes along the way. While I, and many employers, are seeing less meaning in grades, I still don't like that.
- 





## Practically...

You have the green-light to use AI on homework and projects in this course. Pencil-and-paper work, including the in-class problems and exams, are technology-free -- no AI. I therefore encourage you to judiciously AI to debug your work, explain error messages, generate example applications, etc. Additionally, it may be essential to use AI on the machine learning project in this class.

I strongly discourage using AI to write your code from scratch, or even to give you a "skeleton"/outline of the code. It is possible, and many of your colleagues did it in recent semesters. By devaluing this course, they missed out on an opportunity to grow as engineers.
:::{aside}
I am hearing stories about students in tech electives/senior design who are running code, writing down the output on a piece of paper, changing the code and rerunning, writing that result down, changing the code and rerunning, writing that result down, ... . Didn't know how to add the three or fours lines to automate this entirely. I am kinda embarrassed: some of them probably passed my MCEN 3030 course.
:::

## If I am not going to police AI use...

... the responsibility shifts to the students to understand what amount is too much. A good starting point: If you would be hesitant to show me your prompts, you probably went too far.


