<h2> Intro: </h2>
You know that moment when you are learning to program and everything starts to click. You start stringing together methods in what you believe to be this beautiful symphony of functionality. Then, you come across a blog post, article, or book that says, "Actually, don't do that... ." In comes the Law of Demeter (LoD). What?! LoD focuses on the idea of minimizing coupling in your code. Coupling?! Coupling, refers to how objects can call upon each other for some sort of functionality. If I lost you, thats OK, that's what examples are for. Let's dive in.

<h2> The Law of Demeter Example </h2>
Let's imagine a program message chain. It might look something like this:
    
    @printer.print("Hello")

Here I might have created a "printer object" that has a "print" method and I am using it to print "Hello." OK, I'm utilizing an object to print something to the console using the method print. No coupling here! Now lets try to add another object into the loop.

    @printer.print(@greeting.hello)

Now here I have some coupling. Similar to before I have called my printer object to get it's method print, but now I have another object named "greeting" that has a method named "hello," which one might assume returns a "Hello" greeting. Now "print" is taking in a parameter from this object (greeting) and it's method (hello). These objects have been coupled together. They are utilizing each others services in order to create some sort of functionality.

Coupling is a necessity when it comes to functionality of code, but when it comes to breaking LoD that is when your coupling has gone from a necessity to an act of misuse. When is coupling bad? Well, when you are traversing through a great deal of classes in order to gain the functionality of a single method, then you know you might have a design problem. For example:

    @company.get_greeting(@manager.speak(@employee.speak(@apprentice.speak(@greeting.hello)))

Notice how we traversed through multiple methods in order to obtain a single prompt for a greeting. This is problematic and reveals a few things about our code. One, our code interface might not be ideal if we have to traverse through so many methods. In turn, our code may know too much about other classes. No, our code doesn't actually know about other methods per say, but what is happening is your knowledge of this particular piece of software is allowing you to reach out to far distances of classes in order to gain some sort of functionality that you need in a specific spot. It would be better to use code that hides implementation details from another class. What we have done in essence is bind our classes to each other by making these calls. Two, what happens if we happen to change a class or method along this particular path? We'll be in a bit of trouble rewriting all of this code to account for the change. 

<h2> Conclusion </h2>
In the end it pays to decouple long chains of code to avoid pain later. It would be better to utilize an interface that minimizes this sort of chaining as well as creating classes that hide implementation from other classes so that classes don't pick and choose which methods they want to utilize. If we allow this "picking and choosing" of methods this creates an unmanageable web of code if something should change. You lose a great deal of flexbility in your code. Follow LoD the best you can.