<h2> Intro </h2> 
I was recently introduced to the State and Strategy patterns by a fellow apprentice. I found these patterns to be great, especially with a language like Java. In this post I will describe each pattern and provide examples.

<h2> The State Pattern </h2>
The State Pattern is a pattern that is to be used when you have an object where it's actions are dictated by it's state.

Let's look at an example of a play button in an application. Usually play buttons have the ability to pause or play a song, but the icon changes on the button from play to pause. In this example we have two different states. We have one state where the play button could be in a "playing" state or a "standby" state. So we could use a method with conditionals, which contains play and standby logic, but this would make our code "dirty" and it also breaks instances of S.O.L.I.D principles, such as the Single Responsibility Principle.

What might an implementation of this principle look like? Well let's try to diagram what this might look like:

```
_________________
PlayerApplication
-----------------
+setState
+player.action(currentState)
-----------------
       |
       |
_________________
     Player    
-----------------
+action(currentState)
-----------------
    |          |
    |          |
--------    --------
Play        Pause
--------    --------
+action()   +action()
--------    --------

``` 

Here, `Player` can act as an interface to `PlayerApplication`. Given the state during `PlayerApplication`, the state being `Play` or `Pause`, the `Player` interface can take that current state and invoke the action of the `Play` or `Pause` state.

<h2> The Strategy Pattern </h2>
Much like the State Pattern, the Strategy Pattern can also utilize an interface for distinct strategies. Strategies in this case might represent a specific implementation for something to be done. A very odd example might be that you might have two strategies for how you tie your shoe. Some times you may double knot your shoelaces and other times you may tie them normally. Your strategies would be similar in interface to the example above. In fact, the layout would look exactly the same, minus the reference to state. 

<h2> Conclusion </h2> 
Given that these patterns are similar in appearance, we must remember that these patterns focus on differing ideas. The Strategy Pattern is focused on creating an algorithm for each strategy, where as the State Pattern is focused on creating algorithms based upon state of an object. These are great patterns to keep in mind if you should need varied functionality that is interchangeable. 
