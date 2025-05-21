---
title: "Organizing Code"
teaching: 10
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What does it mean to organize code?
- What is a function?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- At the end of this module you should have a better understanding of what spaghetti code is and how to organize it better.

::::::::::::::::::::::::::::::::::::::::::::::::




 From Instructions to Structure: Organizing Code

## What’s a Function?

A function is a set of commands that has a name by which the set of commands can be executed. For instance, let's say you repeatedly want to print three variables called `person_1`, `person_2`, `person_3` like this:
```
print("Hello ", person_1)
print("Hello ", person_2)
print("Hello ", person_3)
```

Instead of copying these three lines and paste them everywhere you want to use them, you can create a function for that and then just call the function.
```
def print_hellos():
   print("Hello ", person_1)
   print("Hello ", person_2)
   print("Hello ", person_3)
```

You can now whenever you want to print the hellos simply use `print_hellos()`.
Functions are a great way to structure your code. They let you keep code together that belongs together and name it, which not only helps making clear what the code is for but also it makes it easily reusable. 

Functions are a great way to structure your code. They let you keep code together that belongs together and name it, which not only helps making clear what the code is for but also it makes it easily reusable. 

When writing functions, however, keep the following guidelines in mind:
- **Keep them small and simple**: the shorter and simpler a function is, the easier it is maintain and to understand.
- **One function, one purpose**: a function should only do one thing, e.g. don't write a function that reads from a file, analyzes it, and then writes to a file. Instead, have one function to read from a file, one function to analyze the data, and one function to write to a file.
- **Prefer fewer arguments**: the more arguments a function has, the harder it is to understand and maintain it.
- **Avoid side effects**: your functions should be structured and written in a way that they do not produce side effects, meaning if you change a function only the function should be impacted. For instance, global variable use is notorious in regards to creating side effects. If your function changes a global variable, then it becomes likely that changes in the function impact other places of your code where you use the global variable
- **Avoid flag arguments**: flag arguments are arguments that hold either true/false values or integers that control the flow of the function. If you pass a parameter (e.g. isRetired) to a function and the only point of the parameter is to use it in an if/else block to control what logic should be executed (e.g. get retirement rate or get the salary of a person) then there is usually a better approach (e.g. creating one function for retirees and one for people still working).

## Keep it DRY

The DRY principle stands for "Don't Repeat Yourself." It means that if you have multiple lines of code that are duplicates of each other then they should be replaced by, for instance, functions. A good indicator that your code could be "DRYier" is if you copy-paste code from one place to another. Using the same code in multiple places by duplicated it means that if you find a bug you have to hunt down all the duplicates and fix it there as well. If you use a function instead, you only have to fix the function (in one place).

## Spaghetti Code

Spaghetti code is code without any structure or modularization. Often that means there are no or few functions or classes to structure your code, but more importantly your code has no discernible structure. Spaghetti code is almost impossible to maintain once it reaches a certain length. 

## Configurations

Configurations should be all kept in one place. For instance if a program needs a few paths to file directories and some numbers (e.g. model parameterizations), then those should be ideally kept in one file named in a way that it is obvious what it contains (e.g. "config" or "configuration"). This way a programmer only needs to find one file to set up a program rather than hunting through the code to find all hard-coded paths and other configurations.

## Keep It Together

Keep the parts of your code that belong together in the same place. Depending on your programming language that can be the same file, or the same class, the same module, or the same directory. You should use whatever means the programming language of your choosing provides to keep code that logically belongs together together. This makes it easier to make changes later on, as you don’t have to look through all the code to find the relevant pieces that need to be changed.

## Whitespace

Whitespace is an often underestimated tool to create structure in code. Lines of code that belong together should be visually together. Similarly blocks of code that address different issues should be set apart. However, one empty line is usually enough to achieve a visual indicator for different blocks of code. More than one empty line typically makes it more difficult to read.

## Know What’s Being Offered

Most programming languages offer a lot of utility functions and solutions for commonly encountered problems. While it takes a lot of time to learn every feature of a programming language, you should first check what solutions are part of the basic functionality of the programming language you are using before implementing your own solution. For instance, if you need to solve a common math problem, first check if your programming language has a math package and if it includes a function that does what you need before implementing your own.




::::::::::::::::::::::::::::::::::::: keypoints 

- Functions can be used to structure code.
- Code that is better organized is easier to understand and maintain.
- Duplicate code should be avoided.

::::::::::::::::::::::::::::::::::::::::::::::::