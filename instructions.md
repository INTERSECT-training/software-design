---
title: "Instructions"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What are some best practices and recommendations to write high-quality code?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- At the end of this module you should have a better understanding of best practices for writing readable and maintainable code one instruction at a time.

::::::::::::::::::::::::::::::::::::::::::::::::





# Layer 1: Instructions

In 2008, Robert C. Martin published his book “Clean Code: A Handbook of Agile Software Craftsmanship”. In this book he lists a set of best practices to write maintainable and sustainable code. We will talk about some of these best practices that are generally very useful. There are a lot of resources out there on clean code if you want to learn more, however, keep in mind that everything has a context and not every recommendation or best practices fits in every situation.

## Naming Things


[![](fig/geek-poke-typo2.jpeg){alt='Geek & Poke - What every good system needs' style="float:right; width:350px"}](https://geek-and-poke.com/geekandpoke/2015/1/12/what-every-good-system-needs)

Naming things is one of the hardest things in programming: you want to use names that are descriptive but not too long. It's an art. What you should absolutely avoid are variable names like `a`, `b`, or `c` and function names like `myfunction` or `do_this`. There are a few exceptions, for example, it can be ok to call your counter in a for-loop `i` but even in those cases there is usually a better name.

Another good rule to follow is to use verbs for functions and methods, for example name your function `calculate` rather than `calculation`, or `retrieve_data` instead of `data`. Variable names on the other hand are usually nouns potentially modified by an adjective, such as `language` or `color`. If you have boolean variables, those are often adjectives or adjectives with the "is"-prefix such as `blue` or `is_blue` (this in part depends on the programming language you are using). 

Lastly, the use of keywords as names should be absolutely avoided. There are few exceptions where it is ok to use a reserved keyword as a name, but those are few and far between. Some programming languages won't let you use reserved keywords as names, however, some do (Python being one of them). For instance, in Python if you name a variable `type`, then the method `type()` will be overwritten and not be available anymore, which can lead in the best case scenario to your program erroring out and in the worst case to produce incorrect results. 

## Searchability

A consideration that should go into naming things should be how well the name would be found if someone searches your code. If you choose function names that have nothing to do with what the functions are doing, it is difficult to find the relevant pieces of code when one is not familiar with it. For instance, if a function that queries a list of temperatures and calculates their average is called `return_value` then searching for "average" or "temperature" won't bring up that method. Similarly, if there are spelling mistakes in names, searches cannot find those either (e.g. if you call a method `calculate_averge` instead of `calculate_average`).



## Consistency

Be consistent! Once you decide on how to do something, stick to it. For example, if you decide to call functions that retrieve values `get_value` (where “value” stands for the name of the variable the function retrieves) then don't start calling them `retrieve_value` half-way through your program. This applies to all levels of development. For instance, if you choose to use type-hints in Python use them consistently throughout your project, not just in one file. Or if you choose to have one file per component then apply this strategy to your whole project. Inconsistent code is much harder to understand, which makes it a lot harder to maintain.

## Indentation

Indentation is an important factor of code readability. So important that in Python, it is part of the syntax of the language. No matter what programming language you use, choose how you indent your blocks (e.g. will you use tabs or blanks, how many blanks will be one level of indentation) and then stick to it. This code:

```
function hello() {
console.log("Hello World!");
saidHello()
if saidHelloTwice(){
console.log("Goodbye")}
}
```

is much less readable than:
```
function hello() {
    console.log("Hello World!");
    saidHello()
    if saidHelloTwice(){
        console.log("Goodbye")
    }
}
```

If you use an integrated development environment (IDE) such as VSCode it will come with some functionality to help you with that. It pays off to make the time to figure out how to set it up in the beginning of your project.

## Magic Numberes

Try to avoid magic numbers. Magic numbers are typically hard-coded numbers (or strings) that you use throughout your code, e.g. you might use Pi by putting 3.14 in multiple places of your code. These values should be put into constants, preferably at the beginning of your code or in a separate file. If you or someone else wants to change one value they should be able to go to one place and change it only once. You don't want to hunt through all code files to find all the places that a certain number is used. Most languages have conventions on how to format constant names (e.g. all uppercase letters) to make it visually clear that a variable is a constant that shouldn't be changed.

## The Principle of Least Astonishment

The principle of least astonishment (or least surprise) basically says that a user (or another developer in the case of code) should not be astonished (or surprised) when using a specific functionality. For programming specifically this means that for example a function should behave according to their name or a variable should hold a value that makes sense given their name. To name a few examples, if a function is called `calculate_average()` it should actually calculate the average and not the mean, or if it is called `get_age()` then it should return the age and not the name of a person. Similarly, a variable called `temperature_celsius` should hold the temperate in Celsius not in Fahrenheit. 

## One Line Should Not Do Too Many Things

Try to keep your lines short(-ish) and let one line of code not do too many things. Except in the case of method chaining (`obj.method1().method2().method3()`), a line should typically do only one or two things. For instance:
```
door = street.houses[0].open() if street.houses[0] and (street.houses[0].is_inhabited() or street.houses[0].is_empty()) else street.move_in().door()
```

There is a lot going on in this one line, which makes it hard to understand. The following is much easier to read:
```
if street.houses[0] and (street.houses[0].is_inhabited() or street.houses[0].is_empty()):
   door = street.houses[0].open()
else:
   door = street.move_in().door()
```

## Commenting and Documentation

Commenting and documentation are its own topic and deserve a lot more attention than this one short pargraph, but for completeness, here are a few recommendations.

- **Don’t comment the obvious.** For instance, the following comment is not particularly helpful:
    ```
    # initializing all the lists
    cars = []
    drivers = []
    ```
    It's clear from the code what's happening. The following edited version is better.

    ```
    # The following two lists keep the currently available cars 
    # and the drivers who need a car.
    cars = []
    drivers = []
    ```
- **Explain the why rather than the how.** For example, instead of commenting that you are adding one to the counter, say why you are doing this (unless it's obvious from your code).
- **Explain the things you might not understand in the future** (an hour, a day, a month… from now) or that might not be clear to other people who read your code.
- **Explain your design decisions** if it’s not obvious from your code (e.g. why did you use an integer flag and not a boolean).
- **Explain why other obvious solutions do not work or you didn’t choose them.**
Keep in mind that your code is not for professional developers and therefore a little bit more detailed comments might be justified.
- **Delete old code, do not just comment it out.** When you comment out code that you don't need anymore instead of removing it, you clutter your code making it harder to pick out the important comments.
- **Adhere to the standards of the programming language.** This will on the one hand make it easier for other people who are used to the standard to read and understand your code. On the other hand, this will allow you to leverage tools such as the ones that are included with your IDE of choice.
- **Make sure your comments are correct.** This might seem obvious but make sure that if you change your code after you commented it that you also adjust your comments. There is nothing more confusing than a comment that the next line does X when it actually does Y.

::::::::::::::::::::::::::::::::::::: callout
## A word on self-documenting code
You might finds statements like the following on website and other programming best practices resources:
* “Self-documenting code is code that doesn’t require code comments for a human to understand its naming conventions and what it is doing.” <br><a href="https://hackbrightacademy.com/blog/writing-self-documenting-code/">Source: Hackbright Academy</a>
* “In theory, the code of a good engineer should be so clear and readable that he simply does not need any documentation.” <br><a href="https://multi-programming.com/blog/self-documenting-code">Source: multi-programming.com</a>
* “Self documenting code is defined as code that explains itself without the need of extraneous documentation.” <br><a href="https://anthonysciamanna.com/2014/04/05/self-documenting-code-and-meaningful-comments.html">Source: anthonysciamanna.com</a>

While it is true that your code should ideally tell the reader something about its purpose through its structure, and variable and function naming, there still need to be comments and documentation to make it understandable and maintainable. The intention of the programmer and the answer to the question "why was this code written the way it is" can in most cases not be conveyed through naming and structure alone.
::::::::::::::::::::::::::::::::::::::::::::::::



::::::::::::::::::::::::::::::::::::: keypoints 

- There are lot of easy to follow recommendations that make your code instantly easier to read and understand (and thereby maintain).
- Writing high-quality code is the first step towards good software design.

::::::::::::::::::::::::::::::::::::::::::::::::