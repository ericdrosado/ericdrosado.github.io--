## Intro
The Transformation Priority Premise (TPP), was proposed in the early part of this decade by Uncle Bob Martin in his blog [post](https://8thlight.com/blog/uncle-bob/2013/05/27/TheTransformationPriorityPremise.html) of the same name. The root of TPP focuses on utilizing simple operations that change the behavior of code during the TDD cycle. The purpose of utilizing these simple operations is to prevent the TDD cycle "impasses" or "long outages" that may occur during the cycle as well as minimize complexity in our code.

Although many understand the implications of TPP's application, which can be determined by how heavily referenced this post is on blogs and books, such as Sandi Metz's [99 Bottles of OOP](https://www.sandimetz.com/99bottles/), not much has been done to address some of the larger questions Uncle Bob raises at the end of his post regarding TPP.

In this post we will review what is TPP, and consider some of the questions that were posed by Uncle Bob in his blog post, and perhaps rejuvenate the transformations into a more pleasant form.

## The Transformations
Below are the transformations that Uncle Bob proposes, in his post, with varied explanations:

| Transformations         | Explanations                                         |
| ----------------------- | ---------------------------------------------------- |
| {} -> nil               | no code at all -> code that employs nil              |
| nil -> constant         |                                                      |
| constant -> constant +  | a simple constant to a more complex constant         |
| constant -> scalar      | replacing a constant with a variable or an argument  |
| statement -> statements | adding more unconditional statements                 |
| unconditional -> if     | splitting the execution path                         |
| scalar -> array         |                                                      |
| array -> container      |                                                      |
| statement -> recursion  |                                                      |
| if -> while             |                                                      |
| expression -> function  | replacing an expression with a function or algorithm |
| variable -> assignment  | replacing the value of a variable                    |

Uncle Bob notes that priority should be given to transformations that are at the top of the list as they are less riskier to transformations on the bottom as they add more complexity to your code. 

In reality, it would be very difficult to just stick to items at the top of the list, and this is where code decisions have to be made. 

## An Incomplete Example with TDD and TPP

Let's consider a simple example using TDD and considering TPP. In this example I will start to create a counter method that can take two parameters, one being an integer and another being an array of integers. We want our counter to count how many numbers in the array are greater than or equal to the number we've provided:

Let's start with the first test:
```ruby
it 'should return 0 for number = 0 and numbers = []' do
  counter = Counter.new
  result = counter.count(0, [])
  assert_equal 0, result
end
``` 
We run the test and it should fail given the fact that we haven't written our class or method. So we create the class and write our method:
```ruby
class Counter
  def count(number, numbers)
  end
end
```
For good measure, let's run the test again to see if our fail message is the same. In this case we should get a message that indicates that our actual value is `nil` and our expected is `0`, which is what we want. Notice that in our transformation list we have used the very first transformation `{} -> nil`. This is clearly the least complex transformation we are utilizing for our code. If we wrote a test that instead provided a larger array of numbers such as `[5, 10, 15]`, we clearly could not use the `{} -> nil` transformation. We would have to add more complexity utilizing other transformations on the list. This is a sign that there is most likely a simpler test. Given that we want to start with the simplest implementation possible, let's get the test to pass with the following:
```ruby
class Counter
  def count(number, numbers)
    0
  end
end
```
Here our test passes, and we did this by utilizing the `nil -> constant` transformation. 

In essence, we should be able to continue this type of TDD utilizing these transformations. Let's set this example aside for now and let's review some of the larger questions Uncle Bob asks at the end of his post.

# The Unanswered Questions of TPP
  There are a number of questions that Uncle Bob poses at the end of his post. Let's take a look at the list:

  ```
  1.) Are there other transformations? (almost certainly)
  2.) Are these the right transformations? (probably not)
  3.) Are there better names for the transformations? (almost certainly)
  4.) Is there really a priority? (I think so, but it might be more complicated than a simple ordinal sequence)
    4a.) If so, what is the principle behind that priority? (some notion of "complexity")
  5.) Can it be quantified? (I have no idea)
  6.) Is the priority order presented in this blog correct? (not likely)
  7.) The transformations as described are informal at best. Can they be formalized? (That's the holy grail!)
  ```

It becomes clear that Uncle Bob has a sense that he is on to something, but can't quite narrow the transformations down. There are still many things to consider. With this I would like to try to test the boundaries of Uncle Bob's TPP list, and start to address some of his questions.

# Uncle Bob's Questions as They Relate to Our Example
Thus far we have introduced a constant to our `Counter` code. Let's take a look at our next test:
```ruby
it 'should return 1 for number = 0 and numbers = [0]' do
  counter = Counter.new
  result = counter.count(0, [0])
  assert_equal 1, result
end
```
We are now adding items to our array of `numbers`. If we run the tests, this test should fail, forcing us to choose another transformation. The question we should be asking is, "which transformation, of least complexity, should I implement next in order to get both tests to pass?" This is where we run into issues with Uncle Bob's transformation list:
```ruby
class Counter
  def count(number, numbers)
    if numbers[0] == nil
      0
    else 
      1
    end
  end
end
```
Notice that I have gone from a constant to a conditional `constant -> if`. There is no `constant -> if`, but Uncle Bob does say that there could be many transformations other than those he has written. On top of that, I would argue that we have also added additional complexity by using the array in the body of our method. I think it is clear that I am being "nit picky," but I am arguing this for what I believe to be good reason. 

I believe the transformation list, in it's current state, holds too much specificity. It would take a very long time to list all of those potential transformations, and even if we had the list, would it be useful as it would be very, very long. On top of that, many languages have different paradigms so how can we account for all those transformations?

I believe Uncle Bob is right to question his work here. Clearly there are other transformations, which he believes to be true, and they could have a wide variety of different priorities. Given that there are many different metrics out there to test code complexity, I doubt that as a community we could come to a consensus on how to quantify these transformations, but perhaps we can come to a generic sense of what TPP is. I believe that we all already have a sense of what TPP is without looking at the list that Uncle Bob provides. 

## TPP, the Generic Approach
I would argue that the fact that Uncle Bob tries to specify the transformations is at the heart of why he questions the TPP list. The TPP list, as introduced, is quite specific and could benefit from a more generic approach to looking at transformation complexity. I propose that instead of thinking about transformations as one construct to another, that perhaps we should think of it as "does the new change in behavior of my code (transformation) represent the simplest implementation possible?" Our writing of specific tests should help us get there, otherwise we may be missing a more specific test. I believe that those who practice TDD already use specific tests and transformations of least complexity innately. In this instance I think we can take the original list and write a generic one that might resemble this innate ability to reason complexity:

| Transformations         |
| ----------------------- |
| No code                 | 
| Constants/Variables     |
| Data Structures         |
| Functions               |
| Conditionals            |
| Iterators               |

You'll notice that each one of these generic items that we can add to our code, to change behavior, condenses and covers most of Uncle Bob's list. The least complex items at the top and the more complex at the bottom. I believe this list can cut across a wide variety of language paradigms, but obviously not all of them. I also feel that this list is a bit easier to understand as a whole.

There are still questions to be asked, such as whether or not this list correctly goes from least complex to most complex, but I do believe it is a step in the right direction to address some of Uncle Bob's questions:

### Are there other transformations?
Definitely, and with this generic list they are most likely encapsulated in one of those transformations.

### Are these the right transformations?
Perhaps there are other transformations to consider, such as the reassignment of variables, but that does not work for all languages.

### Are there better names for the transformations?
I think the generic list explicitly addresses this with constructs that we are all familiar with.

### Is there really a priority? Can it be Quantified?
I do believe that complexity is the right priority here, but again, who is to say that we have the right level of complexity. As I mentioned before, there are a wide variety of metrics, but any one of them could be debated. Perhaps it would be better to just consider the current language and paradigms that we are using to guide our judgment.

### Is the priority order presented in this blog correct?
Again, this could be debated, but I think we should all use our best judgment.

### Can they be formalized?
Unfortunately, I do not think we can formalize a list that can work across all languages and paradigms.

## Conclusion
Although I do believe that there is still a great deal of value in Uncle Bob's transformation list, I do not believe that it should be formalized as "gospel." Instead, I think the list should be used as a template, much like the generic list that was proposed in this post. I believe that those that practice TDD, innately have a sense of transformation complexity, thus the reason why a list of all transformations is not necessary. As we continue to develop our craft we fine tune our TDD practice so that we can ultimately go from very specific tests to generic code. I do believe that at the heart of Uncle Bob's proposal is that every time we change behavior, we should look for the simplest implementation that allows the code to reveal itself and bypass "impasses" and "outages" when writing it.
