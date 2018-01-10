<h2> Intro </h2> 
Another great section in Sandi Metz' <a href"https://www.sandimetz.com/99bottles/"> 99Bottles of Object Oriented Programming </a>, Metz introduces the practice of replacing conditionals with polymorphism. For those who are not familiar with polymorphism, it simply refers to the ability of having many different types of objects respond to a particular message. Metz states, "Polymorphism allows senders to depend on the message while remaining ignorant of the type, or class, of the receiver. Senders don't care what the receivers are; instead, they depend on what receivers do." Given that explanation let's explore replacing conditionals with polymorphism.

<h2> Code Sample Analysis </h2>
If you remember me mentioning before that this book is focused around writing a clean/tested version of the song, "99 Bottles of Beer on the Wall." Below is the class that controls what text is returned during certain times of the main verse of the song. 

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
Notice the ```container``` method where if number equals 1, meaning there is one bottle of beer left, that we are to return "bottle" as oppossed to "bottles." Now, notice that we have similar conditionals for all the methods where number is equal to 0 or 1. This will allow us to abstract out two classes to remove these conditionals.

<h2> Using Polymorphism </h2>
Now, since we have identified some similarities in our conditionals we can isolate them. Let's just focus on the ```quantity``` method. We could create a ```BottleNumber0``` class and set the quantity to be returned as the string ```"no more"```. We could do this through inheritance and implementing a single conditional. We could do that with the following:

```ruby
Class Bottles
  def verse(number)
    bottle_number = bottle_number_for(number)
    next_bottle_number = bottle_number_for(bottle_number.successor)
    # Verse Logic
  end

  def bottle_number_for(number)
    if number == 0
      BottleNumber0
    else
      BottleNumber
    end.new(number)
  end
end

class BottleNumber0 < BottleNumber
  def quantity
    "no more"
  end
end
```

Metz creates a factory here where the correct object is created dependent on the number in the ```bottle_number_for``` method. You can also see that the new ```BottleNumber0``` class inherits quantity from ```BottleNumber``` and overrides the method. This is a great use of polymorphism, which can get rid of every instance where a conditional uses the value "0" to make a decision in BottleNumber.

<h2> Conclusion </h2> 
Using polymorphism to reduce the amount of conditionals you have in your code, really does help with decreasing the size of your classes, but also helps with code quality and readability. If one, wanted to add a feature to the song, this methodology could help, instead of adding conditionals on top of conditionals in the BottleNumber class. An example would be if someone wanted the song to say "Six Pack" for the number 6. You can do this easily with utilizing the following technique.
