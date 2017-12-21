<h2> Intro </h2>
Refactoring at times can generally be a straight forward task on smaller projects, but what happens when you have a much larger project or your client introduces a new feature that you didn't account for. Well, this is when the world of refactoring can be a bit overwhelming. 

At this point of my apprenticheship I have completed a command line based application where a human player can play an unbeatable AI, in Tic-Tac-Toe. Where is the fun in that as the player? Well, I'm sure my clients, AKA my mentors, will throw some additional features on me that will force me to make some tough decisions on design and function. One of those might even be to add varying difficulty to the AI, who knows? But, in order to prepare for the unknown, one should have taken a few steps along the way to insure that these additional features, won't break the code.

In this blog post I will go over a great example, offered by Sandi Metz in her book, <a href="https://www.sandimetz.com/99bottles/">99 Bottles of OOP"</a>, which focuses on where to start and how to approach changing code effectively.

<h2> Let the Open/Closed Principle Guide You </h2>
Metz puts a great deal of emphasis on the Open/Closed Principle, whichis that code should be open for extension and closed to modification. What does that all mean? Well, at the heart of it all you want to be able to add features without modifying your code in a big way. But, in order to accomplish this, your code must be "open." Next we will explore how to open up your code during the refactoring process.

<h2> How to Open Your Code </h2>
Metz goes over a great deal of information in her refactoring chapter, so I want to be clear that I won't be covering every aspect and highly recommend you give her book a read. With that said, how do we "open" our code for extension? Lets look at Metz' example of 99 Bottles:

```ruby
def verse(number)
  case number
  when 0
    "No more bottles of beer on the wall, " +
    "no more bottles of beer.\n" +
    "Go to the store and buy some more, " +
    "99 bottles of beer on the wall.\n"
  when 1
    "1 bottle of beer on the wall, " +
    "1 bottle of beer.\n" +
    "Take it down and pass it around, " +
    "no more bottles of beer on the wall.\n"
  when 2
    "2 bottles of beer on the wall, " +
    "2 bottles of beer.\n" +
    "Take one down and pass it around, " +
    "1 bottle of beer on the wall.\n"
  else
    "#{number} bottles of beer on the wall, " +
    "#{number} bottles of beer.\n" +
    "Take one down and pass it around, " +
    "#{number-1} bottles of beer on the wall.\n"
  end
end
```

Now, if we look at this code we see that we have reached a state of code called "Shameless Green," the code is clear concise and good enough. The issue is, where could we use some refactoring. Metz recommends using code smells as a means to begin your refactoring journey. These smells will not only lead you to a place of refactoring, but also point out where to begin to "open" your code for extension. If we look here you probably notice a great deal of repetition. If we compare the case 2 and the else conditionals, we notice that these two are very much alike. Seems like a good place to start. In order to proceed we will need a good systematic way to go about opening our code.

<h2> Flocking Rules for Duplication </h2>
The flocking rules are as follows:
```
1. Select the things that are most a like.
2. Find the smallest difference between them.
3. Make the simplest change that will remove that difference.
```
So, for step one, what looks alike? Well, we already discussed that the case 2 and else conditionals looks alike. Boom! Next, find the smallest difference between them. At this point we notice that in the case statement, the numbers 1 and 2 are hard coded, while in the else we have a means to change the values by passing a number variable. OK, good. Also, we should notice another detail, which is the fact that "bottle" is used for the case and else uses, "bottles." Now we have an interesting challenge.

Step 3, we want to incrementally make changes, but we must test our code through each change. Nice and steady is the best way to approach this refactor. Well, logically we can change the hard coded values of 1 and 2 and turn change them to be similar to our other code like so:

```
  when 2
    "#{number} bottles of beer on the wall, " +
    "#{number} bottles of beer.\n" +
    "Take one down and pass it around, " +
    "#{number-1} bottle of beer on the wall.\n"
  else
    "#{number} bottles of beer on the wall, " +
    "#{number} bottles of beer.\n" +
    "Take one down and pass it around, " +
    "#{number-1} bottles of beer on the wall.\n"
```

This is great! Remember incremental changes is best so you know if a single change is at fault for failing code. At this point we need to determine how can we get closer to opening our code for extension.

Well we need to tackle our second issue, which is the bottle/bottles issue. Now since these verses are nearly the same, one might conclude that there is a possible abstraction here. The question is how can we build this abstraction.

Well, if we continue to use the Flocking Rules to guide us we want to make the simplest change to this code. Ideally we want bottle to appear when there is only 1 bottle. A great way to accomplish this is abstracting a method. Lets call this method container, because we want to be somewhat generic, and somewhat descriptive. This method could handle what to do given the value of number. How could we call this method... ahh yes, we can utilize string interpolation as seen here:

```
"#{number-1} #{container(number-1)} of beer on the wall.\n"
```

Now we have opened our code to change! Remember, as we proceed we want to make small changes to insure we are abstracting/refactoring correctly. You will probably come to a result that looks like this:

```
def container(number)
  if number == 1
    "bottle"
  else
    "bottles"
  end
end
```

We have now effectively refactored!

<h2> Conclusion </h2>
Refactoring can be difficult, but we can simplify the process by opening up our code for change. In order to open our code we need to identify some code smells to hone in on what we need to refactor. Once there, we can make small incremental changes to get the abstraction we desire!
