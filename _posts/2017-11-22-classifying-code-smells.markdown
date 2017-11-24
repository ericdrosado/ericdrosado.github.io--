<h2> Intro </h2>
I just recently watched a great talk by Sandi Metz titled, ["Get a Whiff of This,"](https://www.youtube.com/watch?v=PJjHfa5yxlU&__s=q1cmrjymtwsbb1tjuymz) which focuses on varying code smells and how these smaller problems can be curatively refactored. Sandi stresses that these code smells are in fact good as they allow us to "surgically" remedy larger problems in our code.

In this post I would like to introduce and define the different classifications of code smells. Sandi mentions that many folks are familiar with the term "code smells," but many can't name at least five smells. In an effort to spread knowledge, I would like to share the names of these smells in their specific code smell classification. I would highly recommend the talk as she even includes an exercise in refactoring.

<h2> The Bloaters </h2> 
The Bloaters classification includes smells that contribute to a large code base that becomes difficult to handle. This groups includes the following smells:

1.) Long Method - A long method. 
2.) Large Class - A large class. 
3.) Primitive Obsession - Overuse of primitives instead of objects.
4.) Long Parameter List - Overuse of parameters for a method.
5.) Data Clumps - Identical groups of variables that appear together.

<h2> The Abusers </h2>
The Abusers are smells that incorrectly use object oriented programming principles. This group includes the following smells:

1.) Alternative Classes with Different Interfaces - When two classes are similar in functionality but do not share the same interface.
2.) Refused Bequest - When a subclass inherits some methods from a superclass only for the sake of reusing those methods and shares no direct relationship to the superclass.
3.) Temporary Field - Temporary Fields is just that, fields that are only used under certain circumstances, and when they are not used are empty.
4.) Switch Statements - When there are a large number or a set of complex switch operators/or conditionals.

<h2> Change Preventers </h2>
The Change Preventers involves smells that make code difficult to change because if you make a change in one place you will have to change code in other locations. This group includes the following smells:

1.) Divergent Change - When multiple changes need to be made in a single class when something in the class is changed.
2.) Parallel Inheritance Hierarchies - Is when you make a subclass for a class, but find that you need to add a new subclass to another class.
3.) Shotgun Surgery - When a single change is made to multiple classes.

<h2> Dispensables </h2>
The Dispensables involve smells where code can be removed to make the code cleaner as it does not need to be in the code base. This group includes the following smells:

1.) Comments - Are just that, comments in the code.
2.) Duplicate Code - Similar code in multiple places.
3.) Data Class - A class that stores data but does not operate on that data in any way.
4.) Dead Code - Code that is not used, but happens to be in the code base.
5.) Lazy Class - Classes that don't do much.
6.) Speculative Generality - An unused class, method, field, or parameter in the code base.

<h2> Couplers </h2>
The Couplers involve smells that contribute to excessive coupling. This group includes the following smells:

1.) Feature Envy - When a method accesses data from another class more than its own data.
2.) Inappropriate Intimacy - When one class uses methods of another class.
3.) Message Chains - When methods chain together through a series of calls in order to complete a class. Think Law of Demeter.
4.) Middle Man - When a class delegates work to another class.

<h2> Conclusion </h2>
The terminology "code smells" is used liberally from my experience. For someone who is still new to the field, I find that clear definitions for these smells have truly helped in my understanding of clean code. I cannot stress enough how great Sandi's talk is when it comes to this topic. I highly recommend it.
