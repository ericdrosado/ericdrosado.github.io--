<h2> Intro </h2>
Recently I have found myself digging deeper into C#. I happen to come across writing LINQ query expressions as a means to write code that is not only very easy to read, but also faster to write. In this post I'll compare the "LINQ Way" to the "Verbose Way" so folks can get a sense of the benefits of using LINQ query expressions.

<h2> LINQ Query Syntax </h2>

<h3> Before LINQ </h3>
Before LINQ query syntax in C# 3.0, folks would have to iterate through collections of IEnumerable<T> by using various loops. So, for example, let's say that we have a list of integers and we want to store numbers greater than 5. Before LINQ, we would have to do the following:

```csharp
	List<int> numbers = new List<int> {2, 4, 8, 16, 32, 64};
	List<int> numbersGreaterThanFive = new List<int>();

	foreach(int number in numbers){
		if (number > 5) {
			numbersGreaterThanFive.Add(number);
		}
	}
```

Well, this code sample is not too complex, but we would expect that ```numbersGreaterThanFive``` would contain the values ```{8, 16, 32, 64}```. 

<h3> After LINQ </h3>
Now that we have a sense of what we would do before LINQ, let's take a look at the LINQ syntax to do the same process in the previous example:

'''csharp
	List<int> numbers = new List<int> {2, 4, 8, 16, 32, 64};
	List<int> numbersGreaterThanFive = from number in numbers where number > 5 select number;
'''

DONE! Notice that the LINQ syntax is short, clean, and is easy on the eyes in the realm of readability. From what I have seen the more common way of writing this syntax would be the following:

'''csharp
	List<int> numbers = new List<int> {2, 4, 8, 16, 32, 64};
	List<int> numbersGreaterThanFive = from number in numbers
					   where number > 5
					   select number;
'''

<h2> Ordering and Grouping with LINQ </h2>
LINQ has some additional features such as ordering and grouping collections. Lets say for example that we have the following collection of birds: 
```csharp

List<Bird> birds = new List<Bird> {
	{Name = "Cardinal", Color = "Red"},
	{Name = "Dove", Color = "White"},
	{Name = "Robin", Color = "Red"},
	{Name = "Blue Jay", Color = "Blue"},
	{Name = "Crow", Color = "Black"},
	{Name = "Starling", Color = "Black"}
}
```

Now let's use LINQ to organize this collection by name in alphabetical order:

```csharp

List<Bird> alphabeticalListOfBirds = from bird in birds
				     orderby bird.Name ascending
				     select bird.Name;
```

The ```alphabeticalListOfBirds``` will have the following stored in the list: ```{"Blue Jay", "Cardinal", "Crow", "Dove", "Robin", "Starling"}```

The new syntax introduced here is ```orderby```, which is the keyword for organization and ```ascending```, which tells how you would like to order your list. You could also use ```descending``` to get reverse alphabetical.

As I mentioned earlier you could also group a collection. Let's use the birds list and group the birds by color:

```csharp
	IEnumerable<IGrouping<string,string>> birdsByColor = from bird in birds
							     group bird by bird.Color;
``` 

This code will save the birds by a "Key" (color) and "Values" (Birds). If we were to loop through this list with a ```foreach``` where we looked for how many birds are in each color group:

```csharp
foreach bird in birdsByColor {
	Console.WriteLine(bird.Key + " " + bird.Count())
}
```
We would get the following: 
```
Red 2
White 1
Blue 1
Black 2
```

The new syntax introduced here is ```group```, which indicates that we want to group a collection and ```by```, which indicates how you want to group the collection.

<h2> Conclusion </h2>
LINQ definitely provides some great tools to manipulating collections in various ways. It is clear that using LINQ queries can clean your code, shorten it, as well as make it easier to read. Defintely worth investigating. 
