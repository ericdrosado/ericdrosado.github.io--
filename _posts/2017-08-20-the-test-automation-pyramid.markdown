<h2> Intro </h2>
I just finished reading Robert Martin's (Uncle Bob), "The Clean Coder." It is pretty much a reflections on his career and a means of him distilling his experience into chapters of information on what lead him to be a successful professional. In this post I wanted to take an opportunity to write about a concept that Martin brings up in Chapter 8: Testing Strategies. Martin argues that in order to be a true professional, you should be kind to those who work in QA, and minimize the issues/bugs that QA finds in your code. In order to successfully do this, Martin discusses how a Professional Development Team should go about implementing, what he calls "The Test Automation Pyramid." The pyramid contains the following: Unit Tests; Component Tests; Integration Tests; System Tests; Exploratory Tests. In this post I'll write about each portion of the pyramid and what it pertains to.

<h2> Unit Tests </h2>
As developers or in my case, future developer, we should all be familiar with the unit test. The goal of these tests is to test the functionality of our code at the lowest level. As good practice, developers should write these tests before writing their code. The benefit of writing the tests first allow you to think simply about the functionality of your future code. You will also find that you write cleaner code by writing these tests first.

<h2> Component Tests </h2>
These tests are written for individual components of the system. The idea is to take a single component of your code and test it by passing input data into the component and gather output data that matches your intentions. Component tests are usually written by those in QA with the assistance of developers. A great majority of the tests focus on happy-path situations and alternate-path situations. All un-happy path cases should be done during Unit Tests.

<h2> Integration Tests </h2>
These tests, test larger systems. The goal is to take multiple components and test the way they interact with each other. The goal is to see how well these components are "choreographed" when it comes to running them together, while mocking or doubling other components. These tests are typically written by architects or lead designers. These tests insure that the architecture of the system is sound.

<h2> System Tests </h2>
System Tests are considered the "Ultimate Integration Test," as they test that the system has been "wired" up correctly and it's parts interoperate as expected.

<h2> Exploratory Tests </h2>
Exploratory tests are tests where developers begin to interact with the system in hopes of discovering any bug or potential issues. This is an all hands on deck affair where the system is scrutinized to the fullest extent.

<h2> Conclusion </h2>
Through my experience at 8th Light I have seen the importance of testing. It is clear that testing is more than a luxury. Every team should invest their time and effort into developing workers with good testing habits to insure the success of the development team as well as the company as a whole.
