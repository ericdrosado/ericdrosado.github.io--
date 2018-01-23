<h2> Intro </h2>
My most recent project involves building a server from scratch. With that, I would like to talk about a very important piece of that server, which are sockets. 

<h2> What are Sockets? </h2>
Imagine the old two tin cans and a string telephone trick, where if two people hold a tin can with a taut string in between them, they can communicate with each other through the tin cans by speaking into the can. Here, the string acts as a means of communication between two people, by allowing one person's words to vibrate along the string and into the other can. This is a simplified explanation as to how this technique works, but you signed up for a socket lesson, not a science lesson. The socket would represent the string in this case, where one can would represent a client and the other can would represent a server.

A socket is simply an endpoint for two way communication between a port from a server and a port from a client. All information between these two locations(client and server) goes through the socket that is bound to a specific port on the machine.

<h2> How do Clients Communicate with a Server? </h2>
Well, the short answer to this question is a socket, but let's talk about how this works procedurally without going into too much detail.

When you go on your computer and you type in a URL to retrieve information from a site you are in fact using sockets! You, as the client, are reaching out to a server, that holds the information that you seek. The server just waits on one end for a client to make a connection request through it's socket on a specific port. When you make a request your machine will also create an access point on a specific port for communication purposes with the server.

Once the connection is made with the server and the server accepts the request, it will bind a new socket to the same port so that the server can listen to other requests. Now, don't worry, this does not mean that the client has lossed it's connection. In fact, the server is now bound to the client's port as a means of continuing communication with it's previous socket.

<h2> What's next? </h2>
Well, there are a lot of things I did not discuss in this post. This post was just a means to introduce the concept of a socket. In reality there are many other components at work such as the TCP layer and HTTP. I would highly recommend finding more reading on these other subjects to get a better understanding of how client/server communication works.

