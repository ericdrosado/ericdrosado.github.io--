<h2> Intro </h2>
Currently in my reading of Sandi Metz', <a href="https://www.sandimetz.com/99bottles/">99 Bottles of OOP"</a>, Metz mentions an idea that has alluded me during my learning of TDD, which is "The Transformation Priority Premise." The basis of this premise focuses on the mantra, "As the tests get more specific, the code gets more generic." Well, what does that mean? Let's use an example from Uncle Bob's blog <a href="https://8thlight.com/blog/uncle-bob/2013/05/27/TheTransformationPriorityPremise.html">post</a> on the subject:

```java
@Test
public void primeFactorsOfFour() {
  assertEquals(asList(),    PrimeFactors.of(1));
  assertEquals(asList(2),   PrimeFactors.of(2));
  assertEquals(asList(3),   PrimeFactors.of(3));
  assertEquals(asList(2,2), PrimeFactors.of(4));
  ...

}

public class PrimeFactors {

    public static of(int n) {
        if (n == 1)
            return asList();
        else if (n == 2)
            return asList(2);
        else if (n == 3)
            return asList(3);
        else if (n == 4)
            return asList(2,2);
    ...
	}
}

```

In the example above you will see a very literal interpretation of TDD at it's finest. Someone would go fail(red) and pass(green) all the way to this point. Now this should appear to be a huge issue for anyone who has a background in programming. There is a great deal of duplication and it is screaming for simplification. As mentioned earlier, the mantra, "As the tests get more specific, the code gets more generic," in this case our code is far from generic and is very specific. This is where the Transformation Priority Premise kicks in.

<h2> The Transformation Priority Premise </h2>
TDD usually travels hand in hand with the common mantra, "Red, Green, Refactor," but Uncle Bob suggests that refactorings have counterparts called "transformations," which are changes that change the behavior of the code. This is in contrast to Refactorings, in that refactoring changes the structure without changing behavior. Uncle Bob ultimately concludes that these transformations are very much a part of the TDD process to prevent "impasses" or "long outages" in the Red, Green, Refactor cycle. 

<h2> The Transformations </h2>
Here is a list of Uncle Bob's transformations:
```
({}–>nil) no code at all->code that employs nil
(nil->constant)
(constant->constant+) a simple constant to a more complex constant
(constant->scalar) replacing a constant with a variable or an argument
(statement->statements) adding more unconditional statements.
(unconditional->if) splitting the execution path
(scalar->array)
(array->container)
(statement->recursion)
(if->while)
(expression->function) replacing an expression with a function or algorithm
(variable->assignment) replacing the value of a variable.
```

The transformations may look like a big much, but they become clear in practice. One idea of this list is that each transformation goes from a specific item to a generic item. So, for the first transformation you can go from "no code at all" to "code that returns nil." Another important idea is that transformations at the top are less riskier to transformations on the bottom as they add more complexity to your code. So, when you go about your Red,Green,Refactor cycle, transformations should be included to evolve code to something desirable or what Metz calls "Shameless Green." Shameless Green solutions value understandability, straight-forwardness, and efficiency. 

Now, as a developer goes through the TDD cycle, as they use transformations, they should try to do so with transformations that are higher on the list, which will yield a "Shameless Green Solution."

So if we reflect on our first example, before we continue to write specific code, we should employ some of these transformations to avoid writing long, duplicated code.

<h2> Conclusion </h2>
As you go through the TDD cycle you should start to include transformations in that process to create Shameless Green code. If you would like to see The Transformation Priority Premise in action, I would recommend this simple introduction <a href="https://www.infoq.com/presentations/tpp-tdd"> here </a>.
