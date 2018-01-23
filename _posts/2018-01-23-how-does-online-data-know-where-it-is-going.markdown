<h2> Intro </h2>
In this post I would like to take a step back and discuss how data is transferred on the internet. I'm sure many, like myself, have used the internet without truly understanding the fundamentals of how it all works. 

If you think of communication over time we have gone from verbal communication with someone who is standing near us to long distance communication with radios and televisions. Having some sort of communication online obviously falls into the category of long distance communication. I would argue that each type of communication is incredibly complex, as it requires some sort of protocol. Obviously, having a conversation with someone next to you seems easy, but at one point you had to learn a language, and you also had to learn the norms involved in having a conversation. Transferring data online is no different in that it too requires some sort of protocol.

<h2> The Data Transfer Process </h2>
I would like to think of online communication in layers. The layers I would like to discuss are the Application, Transport, Internet, and Network layers. I will go through them briefly to give you a better understanding of what is going on when we send data.

<h3> Application Layer </h3>
The application layer is made up of programs you directly interact with, whether online with a browser or a phone app. This layer utilizes what is known as Hypertext Transfer Protocol or HTTP. HTTP is a text based means of communication which follows very specific rules. This layer could also use other protocols depending on what type of application you are using. For example, if you are using an email application you would use the Simple Mail Transfer Protocol or SMTP.

<h3> Transport Layer </h3>
The trasport layer is where Transmission Control Protocol or TCP lives. After the application layer gets the data from the program you are using it interacts with the transport layer through a port. If you are using HTTP this is port 80. TCP will then transform the data into small packets of data. These packets will go throughout the internet to take the fastest route to their destination. Now, you may be thinking this is problematic, because how does the data know how to rearrange itself into the correct order? Well, TCP attaches a "Header" to each packet with instructions on how to put the data back together.

<h3> Internet Layer </h3>
After TCP the packets are pushed into the internet layer, where the Internet Protocol or IP is used to attach the origin and destination IP addresses so the packet knows where it came from and where it is going.

<h3> Network Layer </h3>
The network layer insures that the packets goes to the correct machine the data was intended to go to.

<h2> Conclusion </h2>
This post is obviously short hand at how data is transferred online. It should be known that you could delve much deeper into any one of these layers as I did not go over every aspect. It is my hope that this serves as a basic introduction to helping folks learn the pieces that are at play.
