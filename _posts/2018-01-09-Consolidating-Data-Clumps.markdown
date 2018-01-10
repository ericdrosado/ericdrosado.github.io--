<h2> Intro </h2>
During my reading of Sandi Metz' <a href="https://www.sandimetz.com/99bottles/"> 99 Bottles of Object Oriented Programming </a>, I came across a section that I thought was simplistically elegant, that I thought I should share. This section focuses on "achieving openness" in your code, such that you can extend your code to allow for the implementation of a new feature. With this, Metz focuses on isolating ideas in your code so that it is easier to achieve openness. One such bit of isolation requires the identification of Code Smells and finding the correct remedy for them.

For this post I would like to focus on how Metz approaches instances of "Data Clumping" and how to remedy the situation. Metz admits that her example is a bit of a stretch for this particular code smell, but stresses that removing clumps are beneficial to keeping a clean code base.

<h2> Data Clumping Defined </h2>
Data clumping contains parts of code that has repeated groups of variables. The one example that Metz introduces is the following code in her 99 Bottles verse method:

```ruby
def verse(number)
  bottle_number = BottleNumber.new(number)
  next_bottle_number = BottleNumber.new(bottle_number.successor)

  "#{bottle_number.quantitity.capitalize} #{bottle_number.container}" +
    "of beer on the wall," +
  "#{bottle_number.quantitity} #{bottle_number.container} of beer.\n" +
  "#{bottle_number.action}," +
  "#{next_bottle_number.quantity} #{next_bottle_number.container}" +
    "of beer on the wall.\n"
end
```
Data clumping generally means that you are missing some sort of concept in your code. Especially if you notice that these clumps seem to be passed along together as parameters to different methods. You'll notice in the above code sample, "bottle_number.quantity" and "bottle_number.container" are found paired together for multiple instances. One common way to remove data clumping is to use "Extract Class," which takes the variables and moves them in to their own class, since they seem to share a common relationship. 

<h2> Extract Class </h2>
In the example that Metz presents to the readers, she has already abstracted a class called BottleNumber, which manages attributes of the bottle in the verse such as quantity, the type of container (ex. bottle, bottles, etc), action, pronoun, and successor. The whole class is as follows:

```ruby
class BottleNumber
  attr_reader :number
  def initialize(number)
    @number = number
  end

  def container
    if number == 1
      "bottle"
    else
      "bottles"
    end
  end

  def quantity
    if number == 0
      "no more"
    else
      number.to_s
    end
  end

  def action
    if number == 0
      "Go to the store and buy some more"
    else
      "Take #{pronoun} down and pass it around"
    end
  end

  def pronoun
    if number == 1
      "it"
    else
      "one"
    end
  end

  def successor
    if number == 0
      99
    else
      number - 1
    end
  end
end
``` 

With this Class you can start to see how the verses for "99 Bottles of Beer on the Wall" are constructed. Metz suggests that the clumping in this small example does not need to be extracted into a new class, but the logic can be placed in a method in the BottleNumber class. 

In order to construct this method we have to be able to name what the pairing represents. Metz goes about another means of naming this particular method, but I will attempt to name this bit of clumping and apply the changes. Given that the clump looks at the quantity and the type of container, perhaps we can name the method for this clump as numbered_container_lyric. I use container as opposed to bottle so I can keep the name broad enough just in case the lyrics should change in the future. I do understand that the class has been named BottleNumber, but for the sake of keeping method names abstract, I am going to go this route. 

<h2> Removing the Clumps </h2>
In order to remove the duplicated clumps I am going to create the following method in BottleNumber:

```ruby
  def numbered_container_lyric
    "#{quantity} #{container}"
  end
```

Now that we have this method at our disposal let's apply it to the clumps in the Verse method:

```ruby 
def verse(number)
  bottle_number = BottleNumber.new(number)
  next_bottle_number = BottleNumber.new(bottle_number.successor)

  "#{bottle_number.numbered_container_lyric} of beer on the wall,".capitalize +
  "#{bottle_number.numbered_container_lyric} of beer.\n" +
  "#{bottle_number.action}," +
  "#{next_bottle_number.numbered_container_lyric} of beer on the wall.\n"
end
```
OK, not nearly as elegant as Sandi Metz' implementation: 

```ruby 
def verse(number)
  bottle_number = BottleNumber.new(number)
  next_bottle_number = BottleNumber.new(bottle_number.successor)

  "#{bottle_number} of beer on the wall,".capitalize +
  "#{bottle_number} of beer.\n" +
  "#{bottle_number.action}," +
  "#{next_bottle_number} of beer on the wall.\n"
end
```

Metz is able to achieve this by overriding to_s so her method looks like the following:

```ruby
  def to_s 
    "#{quantity} #{container}"
  end
```
I'll admit that this is incredibly elegant because it reads very well in the verse method in a very Ruby-centric way. 

<h2> Conclusion </h2>
Data clumping can clutter code and create issues down the road, especially if one of the pieces of data accidentally diverges from it's original use. Using these techniques can have a strong impact on code readability, reduce duplication, and helps with building abstractions.
