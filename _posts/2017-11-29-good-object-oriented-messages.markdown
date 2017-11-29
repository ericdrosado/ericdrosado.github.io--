<h2> Intro </h2>
Last time we reflected on Avdi Grimm's newsletter titled, "Alan Kay's Great Mistake," where Grimm focused on the intended use of Object Oriented Design through the use of "messages." In this post I would like to reflect on Grimm's "Four Qualities of a Good Message," but place a much larger emphasis on the third quality, which states that "Messages are one-way." 

<h2> Four Qualities of a Good Message </h2>
Again, Grimm's four qualities of a good message are:
```
1.) Message recipients decide what to do with the message
2.) Recipients can decide to do nothing with a message
3.) Messages are one-way
4.) Messages should use simple formats, such as strings
```
Qualities 1, 2, and 4 are pretty self explanatory. Quality number 3 requires a deeper explanation.

<h2> Tell, Don't Ask </h2>
Quality number three tries to address the idea of dialogue between your objects. Instead of promoting a dialogue you instead want to create a one-way interaction. This one-way messaging is also known as "Tell, don't ask," and it is an object oriented design principle.

The ultimate idea of Tell, Don't Ask (TDA) is that you want one object to give orders to other objects without expecting anything in return. I could relate it to the idea of receiving an invitation to a party. The inviter sends you a message to come to the party, but they don't want to know all the steps that it will take to get you to the party. They just expect you to be there. The inviter does not need to know about your grooming habits or what you intend on wearing....just be there. Similar idea here. Lets look at an example:

<b> Not a Great Message </b>
```ruby
if current_user.is_admin?
  current_user.admin_greeting
else
  current_user.user_greeting
end
``` 
<b> A Better Message </b>
```ruby
current_user.welcome_message
```

So what you might notice here in the "Not a Great Message," is that there is a very clear dialogue happening between two objects. "Are you a admin, if so, I'm going to get the admin greeting, or I'm going to get the user greeting." In our "Better message" we are just simply sending off a "command message" that states, "Pull up the welcome message, and I don't care about how you do it." This is clearly a one way interaction and is at the heart of what Grimm wants us all to implement in our code.

<h2> Conclusion </h2>
The TDA design principle is supported by many folks in the industry. Sandi Metz even goes into great detail in her "Practical Object-Oriented Design in Ruby" book about how TDA can really help clean your code. So, remember, when you are coding with objects, messages are at the heart of object-oriented programming. 
