<h2> Intro </h2>
Structs or Structures are considered a "named type," like Strings, Integers or Arrays. Recently I was exposed to this new tool to add to my quiver of programming knowledge. I read a great tutorial on <a href="https://www.raywenderlich.com/116714/swift-tutorial-introducing-structures">Ray Wenderlich</a>, which goes into great detail on how to declare and use Structs. I would like to pull some of the basics from this tutorial to introduce folks into the wonderful world of Structs.

<h2> Structs! What is it good for? </h2> 
The Wenderlich tutorial introduces Struct with a great example about creating an application that can calculate if a potential customer is within range of a pizza delivery restaurant. In the tutorial they give the following code:

```swift 
let latitude: Double = 44.9871
let longitude: Double = -93.2758
let range: Double = 200.0

func isInRange(lat: Double, long: Double) -> Bool {
    let difference = sqrt(pow((latitude - lat), 2) +
      pow((longitude - long), 2))
    let distance = difference * 0.002
    return distance < range
}
```
Notice that the latitude, longitude, and range have been determined for a single restaurant. What if you introduced other restaurants?! This is where you will require an additional level of abstraction. This is where Structs can come in handy!

<h2> Revisiting our Pizza App with Structs </h2>
I'm going to diverge here from the Wenderlich example, to create a simple Struct for our purposes. I still, highly recommend checking out the Wenderlich tutorial if you get a chance.

Let's create a Struct that allows us to build a pizza location for every restaurant that we would like to add to our app:

```swift
struct Location {
    let latitude: Double
    let longitude: Double

    init(latitude: Double, longitude: Double) {
        self.latitude = latitude
	self.longitude = longitude
    }
}
```

One thing you will notice about Structs is that Structs can have initializers! Woo Hoo! You can use the initializer to set your Location values for each restaurant. How would you do that? Well, you can do it like so:

```swift
let pizzaLocation = Location(latitude: 44.9871, longitude: -93.2758)
``` 

Now, if you need access to these values you can do the following:

```swift
print(pizzalocation.latitude) // 44.9871
```
Now, you could potentially create an array that stores all of these locations without making many latitude and longitude variables for each restaurant.

<h2> Conclusion </h2>
This little introduction only covers the tip of the iceberg of Structs. There are many layers/techniques that one could use with Structs to simplify and clean their code. I would highly recommend looking over Wenderlich's tutorial for more information.
