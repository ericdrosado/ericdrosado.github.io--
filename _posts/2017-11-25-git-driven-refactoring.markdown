<h2> Intro </h2> 
I recently attended RubyConf 2017, and I had the opportunity to see Ashley Ellis Pierce's talk titled, "Git Driven Refactoring," which will be the topic of this blog post. Pierce does a fantastic job discussing how the S.O.L.I.D principles can be correctly implemented using git as a tool for refactoring.

In this post I will discuss git refactoring as it relates to each S.O.L.I.D principle. 

<h2> Single Responsibility Principle Refactoring </h2>
As the name implies, the Single Responsibility Principle (SRP) states that a class should only have one responsibility. Pierce describes that when using git you can easily spot instances where you are breaking SRP by viewing your git log. Lets look at an example that Pierce provided in her talk of a log for a car engine class:
```
e2d1d49 Add hill assist
126e73b Add new remote start devices
1676f99 Allow ability to delay remote start to set time period
8cd0e63 Change current frequency
b983154 Allow user to disable remote start
dedf74c Increase engine power
1a435f7 Allow custom idle time
05e74b7 Add remote start option
```
What you will notice about this git log is that there are many references to "remote start." Pierce describes that because there are many references to remote start in our git log then perhaps it is time to consider creating a new class.

With this, Pierce admits that the only way this will be effective is if git documentation is written well.

<h2> Open/Closed Principle </h2>
The Open/Closed Principle states that a class should be open for extension but closed for modification. Ultimately, the idea behind this principle is that if you are adding new functionality to your code, you shouldn't have to change existing code.

Pierce suggests that if you git diff after adding new functionality, and you notice that your existing code is changing, then you are breaking the Open/Closed Principle. In this instance, you may want to consider adding flexibility to your existing code base so that new functionality can be added without changing the existing code base.

<h2> Liskov Substitution Principle </h2> 
This is an instance where Pierce takes a step away from git and utilizes GitHub. The Liskov Substitution Principle states that every subclass should be substitutable for their parent class. In this case, you shouldn't implement a sublcass that inherits the functionality of a superclass for the sake of reusing certain methods, especially if it has no clear realtionship to the superclass.

Pierce suggests that in order to spot Liskov Substitution Principle violations you can use GitHub linters/bots to identify instances where you may be breaking this principle. For example, Pierce showed the audience a stylebot that the team could utilize to spot instances where it would find, "NotImplementedError," raised in a subclass, which could be an instance where this principle could be violated.

<h2> Interface Segregation Principle </h2>
The Interface Segregation Principle states that many small interfaces are better than one large general purpose interface. Usually this principle is tied to Java, but in the case of Ruby, one could think of this violation in reference to how classes might utilize different class interfaces. A clear example that I found by Luis Zamith on his blog SubVisual, ["SOLID Principles in Ruby"](https://subvisual.co/blog/posts/19-solid-principles-in-ruby/) is if we consider the following:

```ruby
class Car
  def open
  end

  def start_engine
  end

  def change_engine
  end
end

class Driver
  def drive
    @car.open
    @car.start_engine
  end 
end

class Mechanic
  def do_stuff
    @car.change_engine
  end
end
```
Here we have both driver and mechanic using the car interface. Car is serving both of these classes directly and could potentially grow to a class that is over utilized. In reality a driver interacts with the car, but a mechanic interacts with the internals of a car. Thus, it would probably be best to create another abstraction where the mechanic can interact with the internals of the car. 

In order to find such a violation, Pierce suggests using "git log --grep" to locate instances where an interface is being implemented. 

<h2> Dependency Inversion Principle </h2>
This principle states that modules should depend on abstractions, not concretions. Pierce again diverges from git and focuses on GitHub linter/style bots in order to catch these violations. Lets say that you happen to call a class in a method, the bot could identify this and recommend injecting this dependency to avoid breaking the Dependency Inversion Principle.

<h2> Conclusion </h2>
Pierce introduces some neat refactoring tools that can keep you on your game when it comes to SOLID principles. Keeping git and GitHub in mind can really help in avoiding SOLID principle violations.   
