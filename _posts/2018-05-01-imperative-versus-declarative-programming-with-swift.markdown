<h2> Intro </h2>
I've been exploring the functional programming world lately, and I have come across a great introductory resource by Ulisses Almeida, <a href= "https://pragprog.com/book/cdc-elixir/learn-functional-programming-with-elixir">Learn Functional Programming with Elixir</a>. His book has thus far served as an amazing primer for learning functional programming. In it he describes the major difference of OO programming, imperative programming, with functional programming, declarative programming, with the idea that "imperative programming focuses on how to solve a problem" and "declarative programming focuses on what is necessary to solve a problem." At first this description may seem strange so what I would like to do is take a look at Swift through a OO lens and a functional lens and perhaps we can developer a better understanding. For this I will use <a href = "https://www.raywenderlich.com/157123/introduction-functional-programming-swift-2">raywenderlich.com's example</a> in their article, "An Introduction to Functional Programming in Swift." In this exercise a developer is to organize an array of Park Rides by the shortest wait times.

Here is the data:
```
let parkRides = [
  Ride(name: "Raging Rapids", categories: [.family, .thrill, .water], waitTime: 45.0),
  Ride(name: "Crazy Funhouse", categories: [.family], waitTime: 10.0),
  Ride(name: "Spinning Tea Cups", categories: [.kids], waitTime: 15.0),
  Ride(name: "Spooky Hollow", categories: [.scary], waitTime: 30.0),
  Ride(name: "Thunder Coaster", categories: [.family, .thrill], waitTime: 60.0),
  Ride(name: "Grand Carousel", categories: [.family, .kids], waitTime: 15.0),
  Ride(name: "Bumper Boats", categories: [.family, .water], waitTime: 25.0),
  Ride(name: "Mountain Railroad", categories: [.family, .relaxing], waitTime: 0.0)
]
```

<h2> The Imperative Approach </h2>
With the imperative approach you may come up with an algorithm like the following:
```
var ridesOfInterest: [Ride] = []

for ride in parkRides where ride.waitTime < 20 {
   for category in ride.categories where category == .family {
       ridesOfInterest.append(ride)
       break
   }
}

var sortedRidesOfInterest = ridesOfInterest.quickSorted()
print(sortedRidesOfInterest)
```
Now, I will admit that even knowing what the goal of the algorithm was, it still took me a little time to dissect what the algorithm was doing. Now imagine someone who has no context of what this algorithm does and they might need to maintain or debug this code. It doesn't seem terrible, but you'll obviously need to look at the algorithm in detail in order to understand it.

<h2> The Declarative Approach </h2>
With the declarative approach you may come up with the following:
```
sortedRidesOfInterest = parkRides.filter { $0.categories.contains(.family) && $0.waitTime < 20  }.sorted(by: <)

print(sortedRidesOfInterest)
```
At this point you might be thinking, "WOW!" I know that once I saw this I instantly became even more motivated to learn a functional language. Two obvious benefits with the declarative approach are the fact that the code is much shorter in length and it is extremely readable. From let to right I can read the intentions of this code: "I want sortedRidesOfInterest by filtering out rides that are family friendly and have a wait time of under 20. Sort them from smallest to largest wait time." If I were to maintain this code, I would be happy as the functional approach reads very well and will most likely shorten the time it takes to understand the code base.

<h2> Defining Imperative vs Declarative Further </h2>
In the beginning of this post I had mentioned that <a href= "https://pragprog.com/book/cdc-elixir/learn-functional-programming-with-elixir">Learn Functional Programming with Elixir</a> contrasts imperative vs declarative as "imperative programming focuses on how to solve a problem" and "declarative programming focuses on what is necessary to solve a problem." I would like to revisit this further now that we have seen the imperative approach and declarative approach to programming in Swift.

The imperative way of programming clearly focuses on describing each actionable step in order to accomplish the goal. So the imperative way, "focuses on how to solve a problem," by breaking it down to each actionable step and mutating an array of data to store all of the rides of interest. In contrast the declarative way focuses on "what is necessary to solve a problem," by passing along the data and not mutating anything in the process. So what you will see is imperative programming focuses on actionable steps whereas declarative focuses on handling data in order to accomplish a goal/ solve a problem.

<h2> Conclusion </h2>
As you can see, there are very clear benefits to using a functional approach to programming. Besides the fact that you have fewer lines of code, you also should deal with fewer bugs as variables would no longer be mutated with a functional approach. I would highly recommend learning a functional language.


