<h2> Intro </h2> 
Recently I used Enumerations (Enums) while I was refactoring my Swift Server project, and I must say, I was blindsided by how useful they can be. Enums are data type with a set of related values that you as a developer can create. That may not mean much, but let me enlighten you with a few examples.   

<h2> Starting With Enums </h2> 
To create an enum all you have to do is use the following template:
```
enum SomeEnum {
    //Enum definition
}
```
Very simple, but that does not provide a lot of help in explaining what an enum is and how to use it. Let's create an enum that describes the four Cardinal Directions:
```
enum CardinalDirection {
    case north
    case south
    case east
    case west
}
```
Now, we have an enum of Cardinal Direction with four "member values" of north, south, east, and west, where each member value comes after the `case` keyword. So, why is this useful? Well, now we are taking advantage of the Type System. We now have a data type that contains it's member values. The previous code can also be expressed the following way:
```
enum CardinalDirection {
    case north, south, east, west
}
```
You may be wondering, "OK, I have this enum, but I still don't necessarily understand why this might be useful?" Let's explore further the "usefulness" of enums.

<h2> Enum Usefulness </h2>
So I've already mentioned that enum's take advantage of the type system. Simply put, each enum creates a "type" for that enum and it's member values. What?! Take a look at this:
```
type(of: CardinalDirection.self) //CardinalDirection.Type.Type 
```
If we investigate `CardinalDirection` with the `type(of: )` method, we'll discover that `CardinalDirection` is its own type. We could do this with all the member values and we'll see something similar: 
```
type(of: CardinalDirection.north) //CardinalDirection.Type
```
In contrast, let's say that we just want to represent our Cardinal Directions as `Strings`. If we did that, we are allowing Cardinal Direction to be anything that would be considered a `String`. That is not "Type Safe" and could potentially cause issues down the road if someone were to accidentally enter a value later that is not a Cardinal Direction. With an enum, you can avoid that, because if someone were to use a value other than a Cardinal Direction such as `CadinalDirection.foo`, you will receive an error that states `//CardinalDirection has no member foo`. You have saved yourself from a potential headache.  

<h2> Another Use Case </h2> 
Another neat feature of Swift Enums is that you can define a variable in reference to a member type. Here is an example of what this might look like given our Cardinal Direction example:
```
enum CardinalDirection {
    case north
    case south
    case east
    case west
    
    var direction: String {
        switch self {
            case .north: return "North"
            case .south: return "South"
            case .east: return "East"
            case .west: return "West"
	}
    
    }

}
``` 
In this example we have the ability to define a variable that relates to our Cardinal Directions. To call on this variable and receive the return String I would do the following:

```
CardinalDirection.north.direction //"North"
```
Yes, we are introducing a `String` in the mix, but again we are promoting a Type Safe environment as we have already defined the members of this enum. For example, I couldn't call `CardinalDirection.northWest.direction` as it has not been defined in the enum as a member. If a member is not present you will receive an error: `error: Type CardinalDirection has no member northWest`. 

<h2> Conclusion </h2>
As you might have noticed, we have a great deal of control with enums. The Type Safety aspect of using enums is incredibly valuable. I would highly recommend using them in your next project as an alternative to using primitives in your code.
