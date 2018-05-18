<h2> Intro </h2>
Continuing with my exploration of the functional programming world, I've been given the opportunity to explore Elixir. I must say, that my experience with Elixir thus far has been very pleasant. I feel like I've been able to level up quickly with help from Ulisses Almeida's, <a href="https://pragprog.com/book/cdc-elixir/learn-functional-programming-with-elixir">Learn Functional Programming with Elixir</a>.

In this post I would like to engage in a mini code reflection of my Coin Changer Kata. If you are not familiar with the Coin Changer Kata, it is an exercise where the participant practices TDD, by writing an algorithm that when given a value, it can determine the smallest amount of change one should be given based on the amount passed into the algorithm using quarters, dimes, nickels, and pennies. My reflection will look at two versions on my Kata. My first version of coin changer was written earlier in the week, while my second version was written later in the week as I continued to read Almeida's book. Obviously there is much to learn, but for now let's look at these two pieces of code.

<h2> First Version of Coin Changer </h2>
Given that all of my experience with programming has been with OOP, changing mindsets was difficult at first. You can clearly see that my first implementation could just as easily be converted to an OO language: 

```
defmodule CoinChanger do

  @quarter 25
  @dime 10
  @nickel 5
  @penny 1

  def get_coins(change) do
    quarters = div(change, @quarter)
    remaining_change = rem(change, @quarter)
  
    dimes = div(change, @dime)
    remaining_change = rem(change, @dime)
  
    nickels = div(change, @nickel)
    remaining_change = rem(change, @nickel)
  
    pennies = div(change, @penny)
  
    "Quarters: #{quarters}, Dimes: #{dimes}, Nickels: #{nickels}, Pennies: #{pennies}"
  end

end
```

Now, notice that I have one function that is determining the coins I need, with a great deal of duplication for each coin value. For each coin I divide the amount of change I have by the coin value to determine how many coins can I use given the value. Obviously I am going from a larger coin value to a smaller coin value. After that, I determine how much change is remaining after the division. The remaining change value is then used for the next coin denomination to determine how many coins of that denomination can be evenly applied. On the last line I return a string that gives the user the amount of coins for each denomination. 

Here we have a great deal of duplication and no real indication that this could be a functional language to the untrained eye. In this case my knowledge was clearly limited and I was falling back on my previous programming knowledge.

<h2> Second Version of Coin Changer </h2>
After 3 chapters I started to develop a better sense of the power of a functional language utilizing pattern matching, guard clauses, and recursion. Here is my second implementation: 

```
defmodule CoinChanger do

  def get_coins(amount) do
    coin_values = [25, 10, 5, 1]
    coins = coins(coin_values, amount)
    "Quarters: #{Enum.at(coins, 0)}, "<>
    "Dimes: #{Enum.at(coins, 1)}, "<>
    "Nickels: #{Enum.at(coins, 2)}, "<>
    "Pennies: #{Enum.at(coins, 3)}"
  end
  
  def coins([], 0), do: []
  
  def coins([coin | incoming_coins], amount) when amount < coin do
    number_of_coin = 0
    [number_of_coin | coins(incoming_coins, amount)]
  end
  
  def coins([coin | incoming_coins], amount) do
    number_of_coin = div(amount, coin)
    remaining_amount = rem(amount, coin)
    [number_of_coin | coins(incoming_coins, remaining_amount)]
  end

end
```

Here we are starting to see the capabilities of the Elixir language. 

<h3> Functions </h3>

First, I'm sure folks with an OO background are probably thinking, "why in the world do you have functions that have the same name," but if you look closely they have varying arguments as well as guards. So, what is a "guard clause?" A guard clause like `when amount < coin` acts similarly to a conditional, but in this case for whether a function is utilized or not. The guard clause is a very distinct way of telling the difference to functions that may look similar. 

Another way we can determine the differences between similarly named functions is through the usage of arguments. Notice in the first function: `def coins([], 0), do: []` the arguments are an empty list and a 0 whereas the other functions have a list and an amount. When the algorithm is runing it will consider this criteria, when it looks through these functions to determine which one will be used. Think of the three functions as conditionals as well. "If this functions meets the current criteria, use it." 

Now, lets take an opportunity to look at each function and reflect on what they are doing. The first function of `coins` is used if the arguments are an empty list and 0. If this criteria is met it will return an empty list, which can be seen after the `do:`. The second function is used if the amount argument is less than coin, which represents the value of the first coin in the list that is being passed through. If the criteria is met then that means that this particular coin is not divisible into the amount thus this coin will not be used towards the coins that will be given back to the user. To simplify this explanation think about if I had 20 cents, I clearly couldn't use a quarter as a coin, so I will return 0 for quarters. The final line of code is utilizing recursion. Notice the call to `coins` again with new values for the arguments. I am now taking the list of coins that have not been evaluated and passing in the current amount of change I have and in the end returning a list. We will explore this further in a bit.

The final function works the same way as the second function, but we actually do some calculations. Notice that the calculations that are being done are similar to my first iteration of Coin Changer. I am using division and returing a remainder for the remaining amount needed to get the proper change.  

<h3> Recursion </h3>
As I mentioned before, I am using recursion to work through the list I provided, in the first function, `coin_values`. I am going through the list one by one to determine if that value can be used towards determining the correct amount of coins needed for the final change amount. Notice at the end of each `coins` function I am returning a List. So, for the sake of an example, lets say I have 26 cents. What would happen? Here are the steps:

1.) `get_coins` receives the amount as an argument.
2.) `get_coins` calls `coins` and passes the `coin_values` list and the current `amount`.
3.) The first `coins` function is evaluated and given the required arguments, it does not meet the criteria of empty list and a value of 0 for the amount.
4.) The second function is evaluated, but in this case our amount is greater than our first coin, which is a quarter in the guard clause, so we can't use this function.
5.) Clearly the final function is what we need since we did not fit the criteria of the other function, so we determine how many quarters are in the amount of 26.
6.) In the end of the function we will return `[1 | coins(incoming_coins, remianing_amount)]` and the cycle continues for each coin value.
7.) In the end we will end of with the following List after the recursion [1 | [0 | [0 | [1 |[]]]]], which translates to [1, 0, 0, 1], which means that in order to make 26 cents with the fewest coins, we would need a quarter and a penny.
8.) After the recursion we get back to `get_coins` and print out the List into a readable string.

<h2> Conclusion </h2>
In the end we would like our code to be dynamic, but obviously readable. I would argue that the first version was extremely readable, but not very dynamic. If we were to throw in a half dollar in the mix, we would have to write two new lines of code and have to change how quarter is handled as well as the string. For the second version, if we were to add a half dollar, we would have to add `50` to the List and change our final string. Obviously fewer changes, but still changes. I still think I could add better names to the second version, and perhaps handle how my final string is constructed instead of hard coding it, but I'm sure that will come with more experience. Overall, I am enjoying Elixir as well as the functional mindset thus far.



