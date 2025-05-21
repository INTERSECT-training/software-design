---
title: "Introduction"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is software design?
- What is technical debt?
- How are software design and technical debt related?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- At the end of this module you should understand what we mean when we talk about software design and why good software design is important.

::::::::::::::::::::::::::::::::::::::::::::::::


# What is Software Design?

Before we start talking about software design, let’s clarify what that actually means and when you should start thinking about it. You might have written a couple of Jupyther notebook cells before, or a script or two, or maybe you’ve developed a package, or even a web application. All of these things need to be “designed” in the sense that you need to make decisions about where what code goes, how the code flows, or how the user will use your code. While there will likely be fewer design considerations going into creating a Jupyter notebook than into writing a complete web application, that doesn’t mean you don’t need to think about design when creating a few Jupyter cells. If your code is well-designed, it is easier to read, easier to maintain, and easier to sustain in the long-run; either by you or by someone else. 

There are many aspects that feed into designing software and your design choices can affect other components of the software development life cycle. For instance, if you don’t modularize your code, it is a lot harder and potentially impossible to write well-defined tests. Throughout this module, there will be references to other modules with more specific details on a topic. Not every aspect is relevant to every project, but that doesn’t mean they shouldn’t all be considered at some point (even if it’s just to decide to focus on something else).

# Technical Debt

> “In software development and other information technology fields, technical debt [...] is the implied cost of future reworking required when choosing an easy but limited solution instead of a better approach that could take more time.”
> 
Source: [Wikipedia - Technical Debt](https://en.wikipedia.org/wiki/Technical_debt)

Basically, there is not time like the present. If ones chooses saving time over creating a better solution that would require a greater time investment, one accumlutes technical debt. For example, it could be faster to hard-code the paths to files required by a script at the locations when they are needed rather than defining variables at the beginning of a script and use the variables throughout the code. While the first approach would likely be easier and faster at the time of writing the script, it would make it harder to change the file paths for the next project or dataset and require extra work to rewrite the code to enable it to be more flexible.

Technical debt can accumulate at every level of a piece of software from hard-coding strings, to modularizing code, to choosing a database that’s faster to set up but has limited storage capabilities. An important skill for a developer is to recognize when technical debt is accrued and to understand if the effort necessary to pay it down in the future is worth the time saved at present.

Technical debt and software design are interlinked as the better a piece of software is designed, the lower the technical debt typically is. Often a more flexible design takes more time to implement and can be more complex. Hence, it can be tempting to choose a simpler design or to choose to postpone reworking code in favor of quickly finishing a feature. In many cases, however, this leads to a greater time investment in the future.

# The Different Layers of Software Design
Software can consist of many different layers. From writing a couple of lines of code to architecting distributed systems, in each layer the relationship between the different components need to be defined and implemented. For the purpose of this lesson, we will take a holistic perspective on software design and group the concepts and best practices into three layers as follows.

## Layer 1: Instructions
This is the smallest unit of coding: writing instructions that the computer understands. In this context, software design refers to how “things” are named, the code style employed, and how code is broken up into functions and methods. While not everybody might agree that this falls under software design, the decisions you make on this level can have consequences for the whole software.

## Layer 2: Structure and Organization
In this layer, we need to think about where we put the different parts of our code. Questions such as “who can access what functions” or “where does certain functionality belong to” are considered here. Classes or modules can be used to organize code, and considerations about their definition are made here.

## Layer 3: Components and Services
On the highest level, decisions about how different applications and systems talk to each other and how they exchange information are being made. It can also include how the different components of an application are connected. We will not talk much about this layer, but if the applications you develop get to a certain point it should be something you think about.

::::::::::::::::::::::::::::::::::::: keypoints 

- Software design can refer to two things: the structure and implementation of a piece of software, and the plan how to structure and implement a piece of software.
- Technical debt refers to the future cost of reworking a solution that was chosen because it was faster and easier to implement instead of making it more flexible from the beginning.
- When software is not well-designed, technical debt accumulates.

::::::::::::::::::::::::::::::::::::::::::::::::