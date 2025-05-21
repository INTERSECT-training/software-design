---
title: "Components and Services"
teaching: 5
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- How does software design apply to components and services?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- At the end of this module you should have a basic understanding of how to design components and services.

::::::::::::::::::::::::::::::::::::::::::::::::





# Layer 3: Components and Services

We will not talk much about this layer as it highly depends on the type of software you are developing. However, the basic principles we've talked about before apply here as well.

- The responsibilities of your components or services should be clearly defined. Each component or service should ideally handle a specific task (e.g. analyze something or handle notifications, but not do both). However, especially if you opt to set up distributed services (which means that you have multiple applications running to handle different aspects of your overall goal), it will greatly increase the complexity of your applications. Sometimes, it’s the better (or only) choice, but sometimes keeping it all in one application is preferable to avoid too much complexity.
- There should be clearly defined interfaces between components and services. This means on the one hand that they should be well documented, but on the other hand also that there is a limited number of how a component or service can be interacted with. If there are 5 different ways of calling a service with only slight or no obvious differences it makes it a lot harder to understand what the service does and how it should be best used.
- Input and output formats should be clearly defined and ideally use common standards. What this means is that if there is a widely-accepted format that you could use for your data, then use it rather than creating your own. It will make it easier for other people to use your code because they might already have data in the required format or at least are familiar with it. It also means that the output of your code will be easier to use in other programs. 
- Code should not be copy-pasted from one component to another. If you find that two components need the same code, then a third component or package should be extracted with the common code. Otherwise, the likelihood of creating inconsistencies is a lot higher when you for example change one component but don’t apply the change to the other.
- Your components or services should be loosely coupled, which means pretty much the same as it means when we talk about loosely coupled classes or modules. The components or services should know as little as possible about each other’s implementation, and if service A is changed, service B should not be required to change as well. Depending on the type of application you are developing and your use case, there are different technologies and concepts to achieve that such as event buses, microservices, web services, or Functions as a Service.

As a general rule, it’s typically a good strategy to start with the KISS principle (keep it simple stupid) and then increase the complexity as it becomes necessary. For instance, if you build a web application to present data and you don’t know yet how many users you will have or how much data, start with one app on one server. If it turns out that there are too many requests for your application to handle, you can then start thinking about extracting parts of the code into their own services. However, if you already know that you’ll have enough requests to potentially overwhelm one application, then you should design your system in a way that will make it easy to scale it when needed. 




::::::::::::::::::::::::::::::::::::: keypoints 

- The basic principles discussed before apply for components and services as well.
- Loosely couple your components and services.
- Use standards when possible.

::::::::::::::::::::::::::::::::::::::::::::::::