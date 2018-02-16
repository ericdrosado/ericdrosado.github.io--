<h2> Intro </h2>
An understanding of Big O Notation, seems to be a requirement in the software world. With that I have decided to delve deeper into my understanding of algorithms.

Currently I am reading <a href="https://www.manning.com/books/grokking-algorithms">Grokking Algorithms</a> as a bit of an introduction. Thus far, it is a fantastic book that reads in a manner that is accessible to anyone. I found the introduction to Big O Notation to be particularly well written. I would like to share a little bit of what I learned in this post.

<h2> What is Big O? </h2>
Big O Notation aims at telling someone how fast an algorithm is. It does this not based on a specific time measurement such as seconds, but instead in terms of the growth of an algorithm. When I speak of growth, I am speaking in terms of the relationship between the number of items you are running an algorithm against versus the number of operations required to fulfill the task. This is definitely a lot to take in at once, and may seem confusing so let's use simple search and binary search to help us understand this idea.

<h2> Simple Search and Binary Search </h2> 
First, imagine a phone book and let's say you wanted to look up someone's number. What would you do? Would you start at the first page and try to find the person you are looking for. Maybe, if the person's name started with an "A," but what happens if the person's name is John Doe. You could search for John Doe page by page, but that would take a long time. This type of search is called a "simple search." 

In reality, I'm sure you crack the phone book open to a place where you think the name is and make a decision where you go forward in the book or backwards. If we were to build a program to do this for us, we would probably tell the computer to choose the page in the middle of the book and make a similar decision to go forwards or backwards by evaluating where it is relative to the name. The program could continue to divide the sections in half until it get closer and closer and eventually find the name it has been searching for. This type of search is a binary search. 

We already have a sense that binary search would be better than a simple search, but let's explore this with some values using a "Guess My Number" game. Let's say you were given the task to guess a number between 1 and 240,000! It sounds like a terrible, terrible game to play, but what happens if I told you that you could guess the number in at least 18 guesses if I gave you the hint of "Higher" or "Lower" to signify if my number is higher or lower than your guess. How do I know this? Well, we will come back to that in a second.

If we were to guess the number using a simple search, our worse case scenario would mean that we try to guess the number 240,000 times, by literally listing all the number from 1 to 240,000. Not good. If we were to plot this on our imaginery number of items versus the number of operations graph, you would notice that the plot would be a linear expression. Each operation, or guess, would be represented by every number we say and we would say we have a total of 240,000 items to go through.

Now, in a binary search we can half our guesses every time from 240,000. So,
	```
240,000 -> 120,000 -> 60,000 -> 30,000 -> 15,000 -> 7,500 -> 3,750 -> 1875 -> 938 -> 469 -> 235 -> 118 -> 59 -> 30 -> 15 -> 8 -> 4 -> 2 -> 1
	```  

If you notice, we have a total of 18 guesses until we get to 1 number left over. This would be our worse case scenario, but it is definitely an awesome bar trick to find the number in a few guesses. This binary search can be represented logarithmically by log(2) 240,000, meaning log with a base 2 of 240,000 would give us the answer 18. If we were to plot this we would notice that we would have fewer operations using binary as oppossed to a simple search when it comes to the worse case scenario. Our binary search will eventually start to look more and more horizontal over time.

Now, if we compare the algorithms and how they grow, you'll clearly notice that simple search grows linearly, where binary starts to level off over time. If we compared the growth between these algorithms we would see that linear would be the bad choice for an algorithm because it grows, which in turn means it will take more time.

<h2> Conclusion </h2> 
I would highly recommend reading Grokking Algorithms if you are new to programming or concepts surrounding algorithms. It is a great introduction with some wonderful images and examples. It is my hope that while I continue to read this book I will develop some of the baseline knowledge I need to explore some advanced algorithm topics.
