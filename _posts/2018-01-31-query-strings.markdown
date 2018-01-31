<h2> Intro </h2> 
Most of my studying has been focused on the Web. This is mostly due to the fact that I have been tasked with writing a server from scratch. I am starting to see the benefits of such a project, as it gives the person who is building the server an opportunity to truly understand how the Web works.

One little tidbit I've learned, which I never knew about, was that a URL (uniform resource locator) can contain data other than a references to a path. My most recent task was to be able to serve up a personalized greeting in my "Hello World" server using this data, which are called query strings.

<h2> Query Strings </h2>
Let's look at my server address as an example to explain query strings:
```
http://127.0.0.1:3333
```
My server is setup to run locally, thus the reason why I have the "127.0.0.1:3333" for the root of the URL. Now, I can add different paths to my URL, such as:
```
http://127.0.0.1:3333/hello
```
Now, on my server I can parse out the path `/hello` quite simply, which in turn allows me to serve up the following HTML for a browser:
```
<html>
  <body>
    <h1>Hello World<h1>
  </body>
</html>
``` 
This is great, but what if I wanted to change my "Hello World" response with "Hello Johnny". This is where query strings come in. Let's look at a query string in a URL that allows us to deliver "Hello Johnny":
```
http://127.0.0.1:3333/hello?name=Johnny
```
The query is usually separated by a `?`, which in turn allows it to be easily parsed out of the path, followed by a query `name=Johnny`. The query can be parsed out and used in whatever way the developer see's fit, which in my case is to change the greeting to the following:
```
<html>
  <body>
    <h1>Hello Johnny<h1>
  </body>
</html>
``` 

<h2> Conclusion </h2>
There really is not much to be said for the querying that I used, but I thought it was interesting enough to share as many of us see the queries in a web address and don't exactly stop to think what they might do. This is just the tip of the iceberg for query strings, and I hope to discuss the topic further in a future post.
