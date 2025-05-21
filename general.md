---
title: "General Recommendations"
teaching: 15
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are some general recommendations to write better-designed software?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- At the end of this module you should be able to describe some general recommendations to consider when designing software and writing code.

::::::::::::::::::::::::::::::::::::::::::::::::




# Some General Recommendations

The following lists some general recommendations to achive well-designed software. They are rather broad recommendations and can be applied to all layers and many scenarios.

## Code with Intentionality

What this means is that every line of code you write, should be there because it is needed, not because that’s how you have always done it, that’s how you found it somewhere, or that’s how it is in the example. You should understand each line you write and also understand the consequences of it. To give a few scenarios that often result in coding without intentionality:

- We all find solutions and examples on the internet and like to copy-paste those because they solve a problem we encounter. However, make sure you understand what you copy-paste. What does the code actually do that you integrate into your code base? Do you understand what happens in each line and in any given scenario?
- Similarly, if you use an LLM to generate code, make sure you understand the generated code. LLMs are a great tool but they are a recipe for disaster if you blindly copy their solution without understanding it.
- IDEs are also a great tool that can generate code for you. But like all the other scenarios, don’t just use IDE generated code without understanding it.

As a concrete example, consider exception handling. If you catch an exception in your code, why are you doing that? What happens after you catch an exception and does that make sense? Is the rest of the code still executed and if so, would it still be possible to get sensible results? If not, then maybe you should stop the execution at that point. In contrast, if you decide not to catch an exception, what does that mean for your code? WIll it error out? If so, does that make sense or would it still be possible to get valid results if you would catch the exception and continue?

Another example are dates. Dates are often used without considering all the intricacies that they come with. When you display a date, which timezone do you display? UTC? Local time? Your time? And do you show the timezone when displaying it? And if you store dates, do you store which timezone they are in? And does it matter?

## Consistency is Key

No matter what aspect of your code, consistency is always a good thing. Pick a code style and stick to it. Some languages like Python come with a recommended code style, other languages have a number of code styles in use. Google has their [code style guidelines](https://google.github.io/styleguide/) for different languages published if you want to see some examples. Be consistent in how you name variables, functions, classes, methods, etc. If you deviate from your naming patterns make sure it’s a conscious decision and has a good reason. It will make understanding and navigating your code a lot easier.

Consistency also applies to the structure of your application. The more patterns repeat, the easier it is to understand an application. For example, if you use a manager class to manage one type of object, make sure to also create manager classes to manage other types of objects. If you do it one way in one scenario and then a different way in another scenario it becomes easily confusing.

## Documentation

There are many different types of documentation. Not all documentation is or has to be written by the developer and not all documentation is for the developer. Therefore, depending on your project, the requirements for documentation might change with every project as well as over time. The following list lists some common types of documentation.

- Requirements documentation
- Architecture/design documentation
- Technical documentation
    - In-code documentation
    - API documentation
    - Development setup
    - Test documentation
- Installation documentation
- End-user documentation

For many if not most researchers, providing all these types of documentation for a project is not realistic. And often also not necessary! If the code is meant for other researchers to run on their data, we might not need elaborated test documentation or API documentation. However, often at least some aspects of each type of documentation should be written down. Maybe there is no full-blown development setup documentation needed, but at least it should be documented what the dependencies are that need to be installed before the code can be run. Similarly, a full requirements documentation might not be needed but it should be documented what problem the code is supposed to solve.

One way to decide what documentation to write and how much is based on the following two questions:
- **What is most helpful to yourself?**
- **If someone else would help you, what would be most helpful to them?**

If you take these questions as basis for what documentation to write, you'll likely end up with a list that looks something like this:

- Technical documentation
    - In-code documentation
    - Development setup
    - API documentation
    - Architecture/design documentation
- Test documentation
- Requirements documentation
- Installation documentation
- End-user documentation

First you want to make sure you understand your own code. In-code documentation (via comments) is your most powerful tool for this task. Next, you probably want to document how you set up your development environment. What programming language and version, what other dependencies are needed. We have discussed tools how this can be made easier (e.g. using Docker containers). A formal API documentation that documents how the different functions and/or classes and methods can be used will probably be most useful after that, along with an overview of the architecture, the different components of your software. The order of the last four will likely depend on the type of project and who the main users of your code are. Maybe one sentence like "run the test in this way..." will be enough as test documentation and maybe you already have a paper that documents the requirements. Adjust the list above as needed to your particular situation.

In summary, documentation enables yourself as well as other people to reuse your code even when you forgot the details or if you have moved on to different projects. It is a crucial part of software development. 

## Conventions

Many communities have certain programming conventions, for example regarding which code style they typically use, how they test software, or how code is documented. Communities can, for example, be domain specific, programming language specific, or technology specific. Often you will be part of several communities, e.g. the Python community and the computational biology community. Make sure you know the conventions employed by the communities you are a part of and follow the conventions unless you have a good reason not to (intentionality!). It will make it a lot easier for other people in your community to understand the code you write. Sometimes, there might be conflicting conventions in the communities you are part of, in that case it makes sense to consider which community is more likely to read your code or reuse it and use the conventions of that community.

Let’s illustrate this point with the beloved car example. There are certain things when driving a car that once you have learnt them you won’t need to have explained to you again because conventions are in place that it will be the same for all cars. You won’t need to read up on how to open a door, how to use the turn signal, or how to use the break. This is the same for all cars. No documentation is needed (although there probably is some in the manual). Other things however, like the entertainment system, vary from brand to brand, or from model to model. For those, you need documentation to ensure users can use them. And if you choose to deviate from the convention (let’s say you design a Tesla and think how doors open needs to be redesigned), then you definitely need documentation.




::::::::::::::::::::::::::::::::::::: keypoints 

- Every line of code you write should have an intention, a reason it is being written and not just copy-pasted without being understood.
- Be consistent in every aspect of your programming.
- Document what is most important to you first and then go from there.
- Follow the conventions of your community.

::::::::::::::::::::::::::::::::::::::::::::::::