<h2> Intro </h2>
The bind method is an incredibly useful tool that allows you to define the context of a method when called again. I know, that sounds like gibberish. How about the MDN's definition:

"The bind() method creates a new function that when called, has its 'this' keyword set to the provided value, with a given sequence of arguments preceding any provided when the new function is called."

Any better? Well, if you are like me an example is worth a thousand words. In this blog we will go over the bind method to see how helpful it can be to use bind especially if you find yourself getting 'undefined' in the console when calling a method.

<h2> Bind Example </h2>
The following example has been adapted from user 'nkron' on Stack Overflow. Lets say we want to display some information after a button click. First lets define the information that  will be displayed when the button is clicked.

```javascript

Button = function (information) {
  this.information = information;
}

```

So here we want to create a 'this' variable so it can be our parameter for the new function that will be created when bind is called. This way, our 'this' variable takes on the same identity. A little more on this later. Next lets setup our click method and lets create a new button object utilizing our method:

```javascript

var Button = function(information) {
  this.information = information;
}

Button.prototype.click = function() {
  console.log(this.information + ' clicked');
}

var myButton = new Button('OK');
myButton.click();

```

Now here, what would you expect your console output to be? Well, if you guessed "OK clicked" you would be correct. We expect that our information would still be bound to Button. But, what happens if we reassign 'myButton.click'?

```javascript

var Button = function(information) {
  this.information = information;
}

Button.prototype.click = function() {
  console.log(this.information + ' clicked');
}

var myButton = new Button('OK');
myButton.click(); //"OK clicked"

var looseClick = myButton.click;
looseClick();

```

Here we have an issue. By not binding myButton.click, the 'information' that was attached to this.information would be undefined as it is being expressed globally and no longer through myButton.click. The variable in this case is not defined, thus the console print out would be "undefined clicked".

Now lets take a look at what bind can do:

```javascript

var Button = function(information) {
  this.information = information;
}

Button.prototype.click = function() {
  console.log(this.information + ' clicked');
}

var myButton = new Button('OK');
myButton.click(); //"OK clicked"

var looseClick = myButton.click;
looseClick(); //"undefined clicked"

var boundClick = myButton.click.bind(myButton);
boundClick();

```

What happens here is a binding event where the bind method creates a brand new method and passes whatever the 'this' variable is as it's parameter, which in turn keeps the definition of 'this.information' for us. So, we should expect our output in the console to be "OK clicked".

<h2> Conclusion </h2>
Notice how bind can be an incredibly helpful tool when it comes to keeping definitions of variables intact when a method is called from a new object or even if a method is passed from method to method.
