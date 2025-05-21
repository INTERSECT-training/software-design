---
title: "Structure and Organization"
teaching: 30
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- How can code be best organized to make it easier to understand and maintain it?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- At the end of this module you should have a better understanding of how the different parts of code can be connected in a way so your code is better maintainable.
- You will understand what coupling means in software development and how it relates to maintainable code.

::::::::::::::::::::::::::::::::::::::::::::::::



# Layer 2: Structure and Organization

## The Dependency Hell


[![](fig/dependency_2x.png){alt='' style="float:right; padding-left: 10px; width:280px"}](https://xkcd.com/2347/)

Dependency hell refers to the situation in which your code depends on a number of other packages (dependencies) that themselves depend on other packages that depend on other packages, and so on. Some of your dependencies might use the same packages as some other dependencies but a different version of them. Or maybe the dependencies you are using are only available for an outdated version of the programming language you are using and that keeps you from upgrading your code. The more dependencies your code has, the more complex and harder to update it becomes. Therefore, you should carefully choose any package your code *depends* on.

When you choose to use another package, first check who maintains that package and when it was last updated. Is it actively maintained and has a community that reports bugs and makes pull requests? Is it potentially backed by a company? How long has it been since the last release and the last commit? Does the maintainer respond to issues created? By answering these questions, you will get a better sense of how actively maintained the package is. If there hasn’t been much activity in the last few weeks or months, it might be an indicator that the package has been abandoned or will be soon. In that case, you want to be careful about depending on it in your code. If there is not much activity but you still want to use a certain package, then you should be prepared to maintain a fork of the package yourself should it become necessary.

## Code Coupling

In software development, “coupling” refers to how two pieces of code are connected with each other. Coupling happens on a scale from tight to loosely. The tighter two parts of a system are coupled, the more they need to know about each other.

Cleancommit.io defines loose coupling like this:

> “In a loosely coupled system, the components are independent of each other. Each component has its own well-defined interface and communicates with other components through standardized protocols. Changes to one component do not require changes to other components, making the system more flexible and easier to maintain.”
>
> Source: [cleancommit.io](https://cleancommit.io/blog/whats-the-difference-between-tight-and-loose-coupling/)

Tight coupling is the opposite of loose coupling, which means that when you change one component you need to change the other one as well to adapt it to the changes of the first component.

Coupling happens everywhere. Between modules, between classes, between layers, between components, and between whole systems. In a well-designed system, things that logically belong together will be kept together (*cohesion*) and the different components don’t know much about the inner workings of each other but communicate over clearly defined interfaces (*coupling*).


As an example, look at the following code and think about why this is tightly coupled. How could it be more loosely coupled? Then check the discussion below.

```python
def addition():
    num_1 = float(raw_input("Enter Number One"))
    num_2 = float(raw_input("Enter Number Two"))
    addition = num_1 + num_2
    print addition
```

::::::::::::::::::::::::::::::::::::: spoiler 

## Discussion
The function first asks the user to input two numbers. It then adds the two numbers and prints the result. The means of retrieving the two numbers and then add them are tightly coupled as we would have to change this function if wanted the numbers to come from somewhere (e.g. a different calculation). This function can only be used in one scenario, when the user is supposed to enter two numbers that are then added. The following code, achieves the same but decouples the input retrieval from the adding step.

```python
def addition(num_1, num_2):
   addition = num_1 + num_2
   print addition
>
num_1 = float(raw_input("Enter Number One"))
num_2 = float(raw_input("Enter Number Two"))

addition(num_1, num_2)
```

In this code, the function `addition` can be called with any two numbers independent from where those numbers are coming from. If we want to change the code so that the numbers are read from a file, all we need to change are the two lines in which `num_1` and `num_2` are defined.

::::::::::::::::::::::::::::::::::::::::::::::::


## How to know if something is tightly coupled?

You might be wondering how you can know if something is tightly coupled. In theory, it is fairly easy to find out, just ask the following question: If I want to replace component A, do I need to change component B a lot?

If the answer is yes, then your two components are tightly coupled. If the answer is no, then they are loosely coupled. There are degrees of tight coupling, some components are more tightly coupled than others. Similarly, some components are more loosely coupled than others. You won’t always achieve the loosest coupling possible, nor is it always recommendable. This is because, in many cases, coupling two components more loosely comes with the cost of more complexity. And the more complexity there is, the harder it can be to maintain your code.

For instance, look at the following piece of code, does it look familiar?

```python
def addition(numbers):
    total = 0
    for i in numbers:
        total = total + i
    return total

def get_number(question):
    response = raw_input(question)
    num = 0
    try:
        num = float(response)
    except:
        num = 0
    return num

num_numbers = get_number("How many values would you like to add? ")
numbers = []
for i in range(0, num_numbers):
    numbers.append(get_number("Please enter a number: "))

answer = addition(numbers)
print "The answer to the addition is: %d" % (answer)
```

This is the same code from before that adds two numbers. However, it is as loosely coupled as it can be. The different pieces of code are not only loosely coupled to each other, but the code is also loosely coupled to its purpose. It doesn’t have to be two numbers anymore that are being added but can be however many numbers need to be summed up. However, the code got considerably longer and it is a lot harder to understand its purpose. Therefore, you should always ask yourself, do I need my code to be more loosely coupled or more generalized or is this the right balance between loose coupling and understandability?

## Means of Decoupling

The goal of many software engineering best practices is to loosely couple different parts of a system. The following is a (non-exclusive) list of techniques that aim to decouple code (make it more loosely coupled).

- **Information Hiding**
- **Abstraction**
- **Single Responsibility Principle**
- Modularization
- Software Design Patterns
- Well-defined APIs
- Configuration Management
- Dependency Injection
- Microservices

In the following, we will talk about the first three in a little bit more detail.

## Information Hiding 

*Information hiding*, or sometimes also referred to as *encapsulation*, describes the practice of “hiding” the inner workings of a piece of code from whoever calls it. The goal of this technique is to avoid that one has to change the caller when the callee is changed. If calling function A requires knowledge about how A is implemented, it not only tightly couples function A with the code that calls it, it also makes it more difficult to understand the code as looking at the function name and its parameters does not provide all the details needed to use function A.

Some programming languages (like Java or C#) provide means of hiding information that are part of the standard curriculum when the language is taught. Other languages (like Python) offer no or only limited support. Especially in these cases, it is important to learn the standard coding conventions of the language and follow them.

As an example for information hiding, let’s look at the following piece of code. There are two files, one that defines the function `say_something` and one that uses it. If you want to change the animal that makes the sound, you need to know that there is a global variable in `sound.py` that you need to change. 

```python
# sound.py
animal_type = "cat"

def say_something(sound):
    print("The {} says {}.".format(animal_type, sound))


# script.py
import sound

sound.animal_type = "dog" # violates information hiding principle
sound.say_something("bark")
```

The following piece of code hides the information about the global variable. Instead, a function parameter is added that you can use to set the animal. If the implementation of `say_something_animal` changes to for example set a global variable to the passed in value, then the call in `script.py` does not have to change at all. The internal workings of `say_something_animal` stay completely hidden.

```python
# sound.py
def say_something_animal(sound, animal_type="cat"):
    print("The {} says {}.".format(animal_type, sound))


# script.py
import sound

sound.say_something("bark", animal_type="dog")
```

### Object-oriented Information Hiding

More often information hiding is talked about in the context of object-oriented programming. In the following example, knowledge about the internal workings of the class are required to use the class:

```python
class Animal:

    animal_type = "cat"
    sound = "meow"

    def make_sound(self):
        print("The {} says {}.".format(self.animal_type, self.sound))


a = Animal()
a.sound = "hiss"
a.make_sound()
```

As a result, we would be able to rename the variable sound without having to change the code that uses the Animal class. Instead, we can add a constructor parameter, which would allow us to rename the variable as much as we like.

```python
class Animal:

    def __init__(self, animal_type="cat", sound="meow"):
        self._animal_type = animal_type
        self._sound = sound

    def make_sound(self):
        print("The {} says {}.".format(self._animal_type, self._sound))



a = Animal(sound="hiss")
a.make_sound()
```


## Abstraction

*Abstraction* is an omnipresent topic in software development. Very broadly speaking, *abstraction* refers to the result (or sometimes the action itself) of making something less detailed. In programming specifically it refers to removing implementation specific details. For instance, take a math package that offers a function or method to calculate the average of a list of numbers. First it needs to sum up all the numbers, then count how many numbers there are, before dividing the sum by the count. When you use the `average` function, you are using an abstraction, because all you do is call `average()`. Well, in theory at least, but we’ll get to that in a minute.

First, let’s talk about why it is important to talk about abstraction. There are really two reasons. First, every time you program, you create abstractions. The better defined these abstractions are, the easier it will be to maintain the code. You should have a plan for what functions or methods your code will provide. Ideally, the abstractions you create will be consistent and make logical sense (principle of least astonishment!). For instance, if you develop a package to provide domain-specific math functions, then that package should not contain functionality to do string manipulations. 

Second, you are using abstractions every time you program. When you use a module provided by your language of choice or developed by someone else, you are using their abstractions. This means that there is a lot that’s going on under the hood. When using an abstraction, you are trusting that the abstraction is doing what it should be doing and what you think it should be doing. And here is the thing, when earlier it said you don’t need to know the implementation details and that it does not matter to you, that’s not the complete truth. In fact, it does matter because a) you depend on it doing what you expect it to be doing and b) abstractions can *leak*.

### Leaky Abstractions

The "Law of Leaky Abstractions" was coined by Joel Spolsky and states that:

> All non-trivial abstractions, to some degree, are leaky.

Spolsky was a program manager for Microsoft Excel in the 90s, he co-created StackOverflow and Trello, and had a blog [Joel on Software](https://www.joelonsoftware.com/) where he wrote about programming. Some of his blog posts were also published as a book and are still worth reading. 

But what does it mean that all abstractions are leaky? What Spolsky is describing with this law is the fact that as soon as an abstraction is complex enough, the complexity of certain implementation details that abstractions hide bubble up to the higher layers. To use a very simple example, consider the following function that divides two number and subtracts one from it:

```python
def divide_minus_one(num_1, num_2):
	return num_1/num_2 - 1
```

If you use this function and pass in 0 as the second argument you will get a ZeroDivisionError. This means that the implementation specific details (that num_1 is divided by num_2) cause an error that is passed on to the next layer (your code). The abstraction is leaky. To be able to avoid this error, you need to know the implementation details of the function to then handle the division by 0 case in your code.

### Examples of Leaky Abstractions


> Scientists in Hawaiʻi have uncovered a glitch in a piece of code that could have yielded incorrect results in over 100 published studies that cited the original paper.
>
> Source: [Vice.com](https://www.vice.com/en/article/zmjwda/a-code-glitch-may-have-caused-errors-in-more-than-100-published-studies)

In this case, a Python script used for chemistry calculations yielded different results depending on the operating system. Operating systems sort files differently by default (some use alphabetic order, some use the creation date, etc.). The Python script did not take this into account and just used the list of files returned by Python’s functions to get a list of all files in a directory without any further sorting. Since the algorithm relied on a particular order of the files, it returned different results when run on an operating system that sorted files differently. The specifics of the operating system leaked through the Python abstraction and into the script.

Another example is floating point arithmetic. When we are using Python, we typically use the decimal system for calculations. However, numbers are internally stored in a binary system (consisting of 1s and 0s). Not all decimal numbers can be represented as binary numbers. This is similar to not being able to represent certain fractions like ⅓ as a decimal number. 0.1 is a decimal number that can’t be represented as a binary number (it would be a never ending number). This leads on the one hand to rounding errors when your number get too small, on the other hand you might encounter some special cases like the following:

```python
>>> 0.1+0.1+0.1 == 0.3
False
```

In this leaky abstraction, how floating point numbers are represented in the system leaks through to your Python code.

### The Issue with Leaky Abstractions

Leaky Abstractions are really tricky. First of all, you need to know how an abstraction works to be able to handle a leaky abstraction. Often leaky abstractions lead you down the rabbit hole of implementation details in the search for the root cause of an issue. More importantly though, it can be near impossible to know when an abstraction might leak unless you know the implementation specifics of the abstraction. In the case of the chemistry script, unless you have run into the issue of file sorting before or are a very careful reader of documentation (and even that won’t always save you), there is no way of predicting that there might be an issue. This problem is compounded by the fact that the number of existing abstractions increases constantly. The more packages and frameworks there are to make the life of a developer easier, the more abstractions there are, which means the greater the potential for a leaky abstraction. 

## Single Responsibility Principle (SRP)

> “A class should have only one reason to change.”
>
> Robert C. Martin (2003), Agile Software Development: Principles, Patterns, and Practices


Where you could replace “class” with “module” or “function.” This principle is also expressed at: “Gather together the things that change for the same reasons. Separate those things that change for different reasons.” Basically what this means is that the things that belong together should be together. For example, if your module is reading and writing CSV files, then it should not also do math calculations. The only reason for your module to change is if the format of the CSV files changes, for instance. 

While this in theory might seem straightforward, it can get pretty tricky when you have functionality that depends on many different interconnected factors. Sometimes, the question of what qualifies as a “reason to change” needs to be reframed to not introduce too many new complexities in an effort to reduce the “responsibility” of a component.

### Example of Applying the SRP

Look at the following example and think about what the different responsibilities of the class are.

```python
class Student:

    def register_student(self):
        # some logic

    def calculate_student_results(self):
        # some logic

    def send_email(self):
        # some logic
```

In the above example, the `Student` class has three different responsibilities: registering students, calculating the results for a student, and sending an email to the student. This means that it also has at least three reasons to change: if students need to be registered differently, if the results of a student need to be calculated differently, or if emails need to be sent out differently.

The following code separates out those responsibilities into different classes.

```python
class Student:
    def set_address(self, address):
        # do logic

    def set_email_address(self, email):
        # do logic

class Registrar:
    def register_student(self, student):
        # do logic

class EmailService:
    def send_email(self, student):
        # do logic
``` 

Now, each class has only one responsibility. The `Student` class is used to manage student data. The `Registrar` class’ responsibility is to register students (and potentially unregister them). The `EmailService` sends emails. A side effect of applying the SRP is that each class can now potentially be used in a different context (e.g. the `EmailService` could be extended to send emails to faculty).




::::::::::::::::::::::::::::::::::::: keypoints 

- Dependencies need to be managed as well as the code itself.
- *Coupling* refers to what extend the components of a piece of software are connected. Ideally, the components are loosely coupled so that if one component is changed, the others do not have to be changed as well.
- There are many techniques and best practices to achieve loose coupling, information hiding, abstraction, and the Single Responsibility Principle are some of them.

::::::::::::::::::::::::::::::::::::::::::::::::