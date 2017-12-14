<h2> Intro </h2>
I've been reflecting a lot on writing code that is clean, but also flexible when it comes to change. I feel like that this seems to be a great struggle with someone as new as I am to the field. I have a sense of what clean code should be, but flexibility seems to be particularly difficult as I write larger apps. 

Currently in my apprenticeship, I am embarking on an exercise that will test my ability to write clean/flexible code. The process involves writing a command line Tic-Tac-Toe app followed by my mentors adding additional features one by one. The exercise should reveal how clean/flexible my code is as my codebase continues to grow in size. With this, I would like to use this post as a means to discuss what I'm calling "Prepared Simplicity," based on my reading of Sandi Metz' "99 Bottles of Object Oriented Programming."

<h2> What Is Simplicity? </h2>
To me, simplicity is about readability. In my reading, Metz' describes how when we all first started programming we all wrote simple code, which in turn was a strength. In time, our code started to get more complex and in reality, messy, since we knew very little about clean coding practices. Lets not even begin to talk about writing flexible code at this point, because at least for me, it wasn't on my radar until I started my Student Apprenticeship. Well, I am here to tell you that we need to go back and embrace aspects of the simplicity of our past selves. 

Most of our first programs were easy to understand because of its readability. In time, with more complexity added, our code started to become very difficult to read. We didn't name well, we didn't abstract well, the list goes on and on. So we cannot fully embrace our past selves wholeheartedly, because our past selves came with a great deal of flaws. We need to be better prepared for our future selves sake.

<h2> Preparedness </h2>
We all have a sense of the old saying that it is better to be prepared than not, but when it comes to software we have to be careful about how much planning we put into our code bases, as we could create more problems down the road. As Metz' states in her book, "Design decisions inevitably involve trade-offs."

So, how do we strike a balance here. In reality there is no right answer, but there are many things to consider as your write code. For instance, lets look at Martin Fowler's "Design Stamina Hypothesis" with a graph on Metz' blog, titled, <a href="https://www.sandimetz.com/blog/2017/9/13/breaking-up-the-behemoth">"Breaking up the Behemoth"</a>:

![](/assets/posts/2017-12-14-embrace-prepared-simplicity/DesignStamina.png){:class="img-responsive"}

Looking at this graph we can see where good design can payoff in time, as it requires time to build, where as a project with less thought on design will ruin flexibility in the long run. Here we see the give and take, but good design is not that simple. Sometimes, over preparedness can backfire in the sense that perhaps we over plan, and abstract poorly, this could handcuff developers even more. 

Well, if we have to be careful about our preparation, then what do we do? As Metz states in her book, even a well-meaning developer will make mistakes, but to minimize the damage, when it comes to design, you, "should resist [abstractions] until they absolutely insist upon being created." So, in order to be prepared, one must not overplan, but let the code evolve naturally. Resist the temptation to abstract or predict the future, until it is absolutely necessary. To understand when those moments arrive is a lesson for another blog.

<h2> Conclusion </h2>
I truly hope this blog hasn't turned into a rambling, but instead has turned into a warning about over planning. As developers we must embrace simplicity in the sense that we should write our code with clean code paradigms and understand that at any moment abstractions might be necessary to promote good design. I myself have been guilty of drawing out my interfaces before I started to code, but that handcuffed my ability to write flexible code. As I work through my current project, I have tried to apply Metz' idea of writing what I believe to be simple readable code and abstracting when necessary. Thus far it has been helpful, but as I add more features to my Tic-Tac-Toe app, I will truly find out if my code is flexible. 
