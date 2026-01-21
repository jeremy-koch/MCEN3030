# GitHub

GitHub has become the standard location for developers to store, manage, and share their code. An example code collection: [TrackPy](https://soft-matter.github.io/trackpy/v0.7/) is something I found useful when I was analyzing videos from my experiments. The link above is the nice public-facing website, but the code is [hosted on GitHub](https://github.com/soft-matter/trackpy), and you can look around (bottom right) and see that there are 32 contributors to that project.

Imagine trying to co-write code with 31 other people by emailing files back-and-forth! Is there a better way?! Yes -- [git](https://en.wikipedia.org/wiki/Git). GitHub notably uses git as a way for collaborators to seamlessly collaborate on the same project, "pushing" changes from their computers to a shared repository and "merging" those changes to the main branch if they look good and don't conflict with other contributions. Perhaps the coolest thing: you can link this up with your coding environment, sending updates directly from MATLAB/VS Code.

## In this course

We will use GitHub Classroom this semester for homework submissions. In keeping with the theme of letting you choose your own adventure, I outline below two approaches here: a web-browser based method, which requires no downloads, just uploading to the web (similar to what you do for GradeScope/Canvas); and a more advanced approach, which after some initial setup work, will allow you to submit directly from MATLAB/VS Code.
:::{note}
This website was built in VS Code, and I push changes to its repository with a couple clicks in VS Code's left toolbar. Feels good.
:::

Even if you don't embrace it early in the semester, you might consider using it for the machine learning project later.
:::{tip}
If you are proud of your project, you can publish it publically on GitHub and maybe include a link to it in your resume. Additionally... particularly now that AI is around to help, it is easy to put together a website and host it on GitHub. And it doesn't have to look like this one -- plenty of tutorials and templates out there! Maybe you'd be interested in establishing an internet presence, highlighting projects to show future employers...
:::

## GitHub Classroom setup

Canvas will host links to each homework's repository. The first time you click it, it will ask you to pick your account from a list, and then will send your colorado.edu address a confirmation email. Until you accept the invitation in your email, it will tell you that the repository is unavailable. After accepting, that link will show you a webpage with a description of the homework problems and folders for submission. This is YOUR repository (which I hopefully have access to... we'll see this weekend, I guess) -- it should say something like mcen3030-hw1-yourName at the top.

The confirmation step should only be needed once. On future assignments, the links will take you directly to the new homework assignment. 


## Setting up the homework submission pipeline -- Easy mode

You may choose to use GitHub in a straightforward way, with no downloads, no git, none of that. All you need is your internet browser, and you will submit in a similar fashion as you do on Canvas/GradeScope: by uploading.

1. Accept each homework assignment by clicking on the classroom link posted on Canvas.
2. Go to the new repository online (e.g. ```mcen3030-hw1-yourName```).
3. Navigate to the correct folder. For problem one, ```problem_1```.
4. Look for the "Add file" button towards the top right. Select "Upload files", and find your ```.m```, ```.py```, or ```.jl``` file(s).
5. Scroll down to the green "Commit changes" button and click it.
:::{important}
I'm going to say it again: Scroll down to the green "Commit changes" button and click it. If you forget to commit changes, the file is not saved!
:::

This approach is perfectly fine to use for the rest of the semester, and can be your fallback plan if you want to use the integrated method below but have some trouble.

## Setting up the homework submission pipeline -- Harder-at-first-but-ultimately-not-too-bad mode

It is possible to directly link your homework repository to your programming environment, and you can simply click "commit"+"push" to submit. No need to clumsily navigate around on the internet -- submit directly from MATLAB or VS Code! Feels good!

Similarly to above, you will accept each homework assignment by clicking the link, and a new repository will be created under your name. Each will need to be integrated into VS Code/MATLAB -- I'll describe that setup below.
:::{tip}
These instructions may look a bit overwhelming but likely we are talking about a few minutes of work. Submitting homeworks will then be a breeze, quicker than navigating the internet. Plus, interacting with GitHub is a good skill to have -- you could put it on your resume if you get confident with it.
:::

### If you are using VS Code...
... I followed [this tutorial](https://code.visualstudio.com/docs/sourcecontrol/github) to get it set up. There is an overwhelming amount of info there but only part of it is really relevant to us: Prerequisites, Getting started, Cloning a repository, and then there is information scattered about on "committing" (which is to your local repository, as in on your computer) and "pushing" (sending it to the online repository). When committing you have to give a message -- something like "draft of problem 1" or similar is more than sufficient. (Since you don't have 31 collaborators, this isn't a huge deal.)

To emphasize, you will need to commit and push to submit the homework. This is done through the "Source Control" icon on the left toolbar (which should be highlighted after you have made changes). Particularly the first time, and maybe every time, I recommend visiting the web version to make sure your submission made it there.
:::{tip}
Try asking an AI for help or to clarify things. As I was setting up the GitHub Classroom, I asked Gemini things like: "Can students upload their solutions online without needing to use git?" ... and it more-or-less gave the tutorial above. It can really help navigate tutorials, especially when they are bloated with extra things you don't need (as is the case here).
:::

### If you are using MATLAB...

I asked Gemini the following:

> How can I integrate MATLAB with GitHub? I would like to clone a repository, make changes locally, and push those changes back to GitHub.

... and the resulting instructions were much clearer than [the official documentation](https://www.mathworks.com/help/matlab/matlab_prog/set-up-git-source-control.html). (I don't recommend those instructions... the LLM did a better job.) I'll describe what I did here, a bit streamlined from the LLM, but you might try asking an AI yourself. If you need to clarify anything along the way, it can help!

Prerequisites:
1. Install Git: download from git-scm.com. You can try step 2 here first if you think you might have it -- you might, e.g. if you have worked with Python before. (I had it already. Mine came from the Python package manager, hopefully installation via that website is good.)
2. Verify Installation: In the MATLAB Command Window, type the following to ensure MATLAB can find Git: ```!git --version```. If it returns a version number, you are ready to proceed.

Getting a repository:
1. Home -> New -> Git Clone. You can also do Project.
2. It will ask for a URL. That is the web address of your repository, e.g. https://github.com/your-name/mcen3030-hw1-yourName. (This is generated after you accept the assignment.)
3. You can change the folder destination within that menu if you'd like, but don't have to. After a few seconds, your workspace ("Files") should switch to a local version of the repository.

You can then make changes locally. Create your .m files in the appropriate folders, etc. When you are ready to commit a draft or final version of your code to the online repository.
1. Right- or control-click on each of the new files you created and go to "Source Control" -> "Add to Source Control".
2. Right- or control-click in the white area within your workspace (beneath the files) and go to "Source Control" -> "Commit". You have to provide some comment about what the commit is, something like "first draft of problem 1" is reasonable. (Since you don't have 31 collaborators, this isn't a huge deal.)
3. Then, back into "Source Control", but this time choose "Push". It will ask for a login name and token. Leave it here for now.

Getting a token takes a couple steps in your web browser.
1. Go to www.github.com
2. Top-right there is an avatar (which you can change, by the way). Clicking it opens a menu -- choose "Settings".
3. In the list on the left side, at the very bottom, is "Developer Settings".
4. From there, you can choose "Personal access tokens", and then "Tokens (classic)", and then in the middle of the page you should see "Generate new token". Click on that and choose "Generate new token (classic)".
5. A complicated-looking set of choices will pop up, but the only thing you need to turn on is "repo". Scroll to the bottom and click "Generate Token", and then the next page will give you a long password-like thing. That is what you paste-in to go alongside your login name. Probably you will use a six-month token, which will give your MATLAB access for six months... you should only have to do this one time this semester.
:::{important}
The token is like a password and should be a secret.
:::



### If these sound like too much...

No problem, just skip back up to "Easy mode" above. You can submit online for now and get this set up later, or never get it set up and use the online submission forever. 