<h2> Intro </h2>
On my previous <a href= "https://ericdrosado.github.io/2018/01/11/querying-with-LINQ.html">post</a> I wrote about writing clean, easy to read, truncated code using LINQ query expressions. What happens if I said, you can continue to condense your code even further using LINQ method syntax with the help of lambda expressions. Well Ladies and Gentlemen, it's possible.

<h2> Comparing Syntax </h2>
Let's look at the same example I used in my previous post: 

```csharp
	List<int> numbers = new List<int> {2, 4, 8, 16, 32, 64};
	List<int> numbersGreaterThanFive = new List<int>();

	foreach(int number in numbers){
		if (number > 5) {
			numbersGreaterThanFive.Add(number);
		}
	}
```
The "verbose" LINQ syntax that would accomplish the same as the above would be:

'''csharp
	List<int> numbers = new List<int> {2, 4, 8, 16, 32, 64};
	List<int> numbersGreaterThanFive = from number in numbers
					   where number > 5
					   select number;
'''

Now, we can continue to simplify this LINQ syntax using Lambda expressions, which are anonymous functions. The following code uses a Lambda expression to accomplish the same as the above LINQ example:

```csharp
	List<int> numbers = new List<int> {2, 4, 8, 16, 32, 64};
	
	numbers.Where(number => number > 5);
```

You should notice that there is a familiar keyword in ```Where```, which accomplishes the same thing as ```where``` in the other LINQ syntax.

Let's take a look at the Lambda expression further and dissect it. Lambda expressions have three parts: input parameters, a lambda operator, and an expression. ```number``` on the left side of the lambda operator, ```=>```, is the input parameter. The valuesof ```numbers``` are passed into ```number``` and evaluated by the expression ```number > 5```.

<h2> Ordering </h2>
Yes, you are able to order values using the LINQ method syntax with the help of lambda expressions.

If you wanted to order the numbers stored in ```numbers``` you could do the following:

```csharp
	List<int> numbers = new List<int> {2, 4, 8, 16, 32, 64};
	
	numbers.OrderBy(number => number);
```
<h2> Chaining Methods </h2>
Let's bring back the Bird example from the previous post and explore ordering birds by color and then make sure they are ordered alphabetically. We can do this by chaining our methods like so:


```csharp

List<Bird> birds = new List<Bird> {
	{Name = "Cardinal", Color = "Red"},
	{Name = "Dove", Color = "White"},
	{Name = "Robin", Color = "Red"},
	{Name = "Blue Jay", Color = "Blue"},
	{Name = "Crow", Color = "Black"},
	{Name = "Starling", Color = "Black"}
}

birds.OrderBy(bird => bird.Color).ThenBy(bird => bird.Name);

```

Here we use ```ThenBy()``` to insure that our previous ordering is preserved. If we used two ```OrderBy()``` methods, the last ```OrderBy()``` will be expressed as your final ordering.

<h2> Conclusion </h2>
LINQ method syntax coupled with Lambda Expressions can be a great help in writing code quickly. The condensed code is also an added benefit. Queries with LINQ can be done quickly, cleanly, and with fewer lines of code.
