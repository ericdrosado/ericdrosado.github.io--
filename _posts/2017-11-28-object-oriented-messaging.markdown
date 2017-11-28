<h2> Intro </h2>
A few weeks ago I signed up for a newsletter by Avdi Grimm titled, "Lies of Object Oriented Programming," which has been a very informative newsletter. So much so that I would like to share something that is not entirely new to me, but definitely something that I have struggled to implement well, which is the idea of "messaging" in programming. 

In the newsletter titled, "Alan Kay's Great Mistake," Grimm argues that there is a huge misconception behind what the core value of Object-Oriented programming is. Grimm argues that we shouldn't focus on Objects, but instead <b>messages</b>. I'm sure we have all sent messages in our code from one object to another, but I'm sure we are also guilty of returning data with those messages. 

In this post I will discuss some of the information presented by Grimm as well as information from some other familiar names in understanding why we should be placing a greater emphasis on messages as opposed to objects.

<h2> Alan Kay </h2>
Alan Kay, a computer scientist and creator of Smalltalk amongst many other things, created and coined the term Object-Oriented Programming. In 1998 Kay sent out an email that stated:

```
I'm sorry that I long ago coined the term "objects" for this topic because it gets many people to focus on the lesser idea.
``` 
He later goes on to say:

```
The big idea is "messaging"
```

Kay shows a great deal of concern for what he believes to be the biggest missed point of his invention. Messages are at the foundation for Object Oriented Programming. So, how do some of us find our way back to utilizing this tool in the way it was intended to be used?

<h2> Finding our Way Back </h2>
Sandi Metz has been speaking about Object Oriented Design at conferences since 2009. She has explained that her thoughts about this topic stem from her idea of what she would tell her younger self based upon what she knows now. Thankfully she has shared that knowledge with the community as well. In her Practical Object Oriented Design in Ruby book, she states that we should all strive to create message based applications. She also states that applications and their interfaces are defined by the messages that are passed between objects. She says:

```
When messages are trusting and ask for what the sender wants instead of telling the receiver how to behave, objects naturally evolve public interfaces that are flexible and reusable in novel and unexpected ways.
```

So, in order to find our way back, Grimm introduces four qualities of a good message:

```
1.) Message recipients decide what to do with the message
2.) Recipients can decide to do nothing with a message
3.) Messages are one-way
4.) Messages should use simple formats, such as strings
```

<h2> Conclusion </h2>
With messages being at the forefront of Object-Oriented Design, I would like to continue this thought process in another blog post that explores Grimm's Four Qualities of a good message. With this we will also explore "Tell, don't ask," a popular design principle.
