<h2> Intro </h2>
In the past I have worked through a variety of tutorials involving Javascript, and I have also made a few small projects along the way. This time around, I found myself particularly interested in the concept of "this," as it still alludes my understanding completely. This post is an attempt to summarize 'this' basics from a great article I found called <a href="http://javascriptissexy.com/understand-javascripts-this-with-clarity-and-master-it/">"Understand Javascript's 'this' with Clarity, and Master It."</a>

<h2> Think of 'this' as a Pronoun </h2>
In case you need a refresher on the meaning of a pronoun, it is a word that substitutes for a noun, a person, place, or thing. A few examples would be he, she, or it. They take the place of a noun for simplicity and prevents sentences like: "Eric likes to run because Eric enjoys exercise." The more accepted sentence structure would be: "Eric likes to run because he enjoys exercise." Now, as a reader you understand the context of 'he' because it clearly relates to the noun 'Eric.' Now, 'this' works in a similar fashion. Lets take a look at an example:

```javascript
var pet = {
  type: "Dog",
  name: "Wrigley",

  petDescription = function() {
    console.log(pet.name + " is a" + pet.type);
  }
}

```

Now notice that within the petDescription function we call out to the pet object to obtain it's properties 'type' and 'name.' No big secrets exposed here, but this is a prime opportunity to utilize the 'this' keyword as our "pronoun:"

```javascript
var pet = {
  type: "Dog",
  name: "Wrigley",

  petDescription = function() {
    console.log(this.name + " is a" + this.type);
  }
}

```

Now, seeing this code we have a sense for the context of 'this' because the function is a property of our pet object. So in this case 'this' clearly refers to 'pet.'

<h2> Using 'this' Globally </h2>
When utilizing 'this' through a global scope we have to understand that 'window' will represent our global object, unless in strict mode. So, lets take a look at the following:

```javascript
var type = "cat",
  name = "Rhino";

  petDescription = function() {
    console.log(this.name + " is a" + this.type);
  }

var pet = {
  type: "Dog",
  name: "Wrigley",

  petDescription = function() {
    console.log(this.name + " is a" + this.type);
  }
}

petDescription();
```
If we called the petDescription function outside of the pet object, what do you expect to get for your pet description? Well, you would get "Rhino is a cat" as your description as opposed to "Wrigley is a dog" in this particular case. Because we are running petDescription in a global context we are essentially saying 'window.petDescription'. If I wanted to get "Wrigley is a dog" I would have to call 'pet.petDescription()'.

<h2> Conclusion </h2>
Thinking of 'this' as a pronoun greatly simplifies the concept of 'this'. I still highly recommend reading  <a href="http://javascriptissexy.com/understand-javascripts-this-with-clarity-and-master-it/">"Understand Javascript's 'this' with Clarity, and Master It"</a> for additional clarity and helpful tips. Otherwise, this is enough of 'this' to get you through your first JS project.
