<h2> Intro </h2>
I have had the opportunity to partake in <a href="https://cucumber.io/training">BDD Kickstart</a> earlier this week, and I would like to share some of the ideas I was exposed to pertaining to Behavior Driven Development, also known as BDD. BDD is the practice of taking time before development to describe how the team wants a system to behave. This practice includes all the major stakeholders such as "the business", developers, and testers. These three are the recommended participants, but there could obviously be others. The clear benefit of doing this is to ensure that the stakeholders understand the acceptance criteria for the project. 

I would like to talk through the fundamentals of the BDD workflow. This workflow can be broken down to three phases, which include a discovery, formulation, and automation. 

<h2> Discovery Phase </h2>
During the discovery phase the stakeholders meet together to discuss the requirements for the new project. The Discovery Phase utilizes collaboration through a structured conversation, which in turn promotes a shared understanding between stakeholders. The recommended "structured conversation" format introduced during the workshop is known as "Example Mapping." 

Example Mapping is a discovery technique that was created by Matt Wynne. The basis of this process is to use concrete examples to help explore the particular system, which in turn becomes the basis for acceptance tests. The examples alone are not enough during this example mapping process. Each mapping process should include a story, rules that govern that story, examples, and questions that might arise during the conversation.

As an example, lets consider the development of software for an ATM machine that dispenses 10's, 20's, and 50's. The customer wants the following:
```
I want to receive a mix of bills when I withdraw cash from the ATM
```
The above could constitute as a "story." So, what are the specifications or "rules" that govern this? Let's say that one rule is at least one 10 is given for each transaction. So far we have the following:
```
Story:
I want to receive a mix of bills when I withdraw cash from the ATM

Rule:
At least one 10 is given for each transaction.
``` 

Now we have a story and a rule. This information can be brought into a meeting with our stakeholders where they can have a conversation about this information to insure everyone is on the same page. The story and the rule are shared in this meeting, and from there the stakeholders can develop examples that fulfill the story and the rule. 

Examples should be structured in a way that explains the context of the situation, an action, and an outcome. For an example of an "example," would be something like the following:

```
Context:
The ATM contains 10 x 50's, 10 x 20's, and 10 x 10's
Action:
A customer requests $40
Outcome:
Bills dispensed as a 20 and 2 x 10's
``` 

Now notice that we are describing the behavior for this specific example. We are being as concrete as possible so each stakeholder understands what is going on. This example not only satisfies the story, but it also follows the rule. Great! Let's come up with another example:

```
Context:
The ATM contains 10 x 50's, 10 x 20's, and 0 x 10's
Action:
A customer requests $40
Outcome:
??
``` 
Here we have an issue. This example doesn't have a clear answer as it is unable to fulfill the rule that we have established, since the ATM does not contain 10's. This could be an instance where we scrap the example and write a question:

```
Question:
What do we do if 10's are not available?
```

In this instance we have an edge case that needs to be addressed. For now we can put this portion of the story on hold. In order to keep the meeting going we can discuss other rules and develop examples and continue to ask questions. Questions can be saved at the end of the meeting and can be sent back to the client for answering. Once these questions are addressed they can be developed into new rules for the next iteration.

You might be able to see the benefits of such a process. Every stakeholder can see the behavior written out as opposed to be written out in code. We can insure that everyone has a clear understanding of what needs to be accomplished to avoid pitfalls.  

<h2> Formulation Phase </h2> 
During the formulation phase the story, rules, and examples help to build documentation for the project. These examples of the systems behavior are documented using business terminology so that all stakeholders understand the core system behavior. In this instance the context, action, and outcome for each example can be formulated into Gherkin syntax. 

Gherkin syntax is a "stakeholder readable" language that lets you describe software behavior without going into the programmatic detail of how to implement the behavior. Cucumber, a BDD specific tool, uses Gherkin to write and document acceptance tests.  

Lets say our stakeholders managed to have a successful meeting and were able to outline multiple rules and examples. They might come up with the following Gherkin for our ATM machine:
```
Scenario: Withdraw from ATM 
Given I have an account 
and I want to withdraw money
When I withdraw 20 dollars
Then I should receive 2 x 10's 
```

When is comes to Gherkin syntax there are a few things to consider about how Gherkin is structured. Lets look at another example for comparison:

```
Scenario: Withdraw from account and credit is reduced
Given my account has a balance of $100
When I withdraw $25
Then my account balance should be $75
```

Now you should notice some similarities between these two Gherkin examples. You should see a set of reoccurring words as well as a certain order to how those words appear. Some of the common words in Gherkin are scenario, given, when, and then. Obviously there are other word similarities, but that is because of the context of the examples, such as the word, account. In Gherkin, the words given, when, and then are the primary means to explain and document the functionality of a system. You'll also notice that between the two examples there is the usage of "and," which is intentional. You can use "and" to string together additional information that might relate to a Given, When, Then situation. For example:

```
Scenario: Update balance after deposit for two accounts
Given I have an checking acount with $100 and a savings account with $200 
and I want to deposit money
When I deposit $10 into checking 
and I deposit $10 into savings
Then my checking account balance should be $110 
and my savings sccount balance should be $210
```

Writing clear concise Gherkin is a skill to master over time, as you don't want to write too much logic into a single example. You want to have examples that are clear to the reader, a clear example to implement for a developer, and easy to test for a tester. 

If you write enough of these scenarios you will have a great deal of documentation for any team member. With software like Cucumber you can take this syntax and create acceptance tests, which is where we are going next.

<h2> Automation </h2> 
The automation phase focuses on "automating" the documentation, which essentially means that we can create a living document, by turning this documentation into tests. Now, here is the beauty of using Cucumber. Cucumber allows you to take your Gherkin syntax and package it with your system as tests. Why is this such a huge benefit you might ask. Well, think about it this way. Documentation can potentially live anywhere. With that you could comment in your code or have it written in a README of sorts, but who is going to update that documentation? Maybe you change something where a comment is placed and forget to update the comment. Whoops! That's problematic. Or lets say you make a change and you forget to update the documentation to reflect that. Another mistake. With Cucumber, you have the documentation and if you change something, guess what, your tests could potentially fail. In this case you will either need to change your code or update the document. At this point if you want to make sure your code is in the green, you must update the documentation! Coupled with Cucumber you could also add additional unit tests to ensure your system behaves as intended. 

<h2> Conclusion </h2>
BDD is a powerful collaboration tool. BDD coupled with Cucumber and TDD can be an incredibly powerful tool, but only if you have buy in from your organization. I highly recommend attending a BDD workshop and seeing if this is something your company can implement as it can help streamline the development process with the involvement of stakeholders from different departments.
