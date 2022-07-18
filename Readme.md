### 1- What is Webserver ?

- "A web server is software and hardware that uses "HTTP" (Hypertext Transfer Protocol), and other protocols to respond to client "requests" made over the World Wide Web.

==> The main job of a web server is to deliver website content to users."

- Resource: https://www.techtarget.com/whatis/definition/Web-server -

It means that the "web server", is first of all a "server" which means a hardware
The word "web" linked to the word "server" specify that the job of this server is to deliver website content to users.

The second important thing to mention, is "HTTP" (Hypertext transfer protocol),
==> The web server can support other protocol like "SMTP" for "Simple Mail Transfet Protocol" and "FTP" for File Transfer Protocol, used for email and file transfer, besides the "HTTP protocol".
	
	---------------------------------------------------

### 2- What is the HTTP protocol ?

In the OSI Model, the HTTP protocol remains in the "Application Layer".
For more information, check the link below.
- Ressource: https://medium.com/geekculture/understanding-http-protocol-osi-model-ba57cd5bda14 -

"HTTP is a set of rules for transferring files -- such as text, images, sound, video and other multimedia files -- over the web.
==> As soon as a user opens their web browser, they are indirectly using "HTTP".
==> HTTP is an "Application protocol" that runs on top of the "TCP/IP" suite of protocols, which forms the foundation of the internet.
==> The latest version of HTTP is "HTTP/2", but IT DOES NOT make her predecessor "HTTP 1.1" OBSOLETE." 

- Resource: https://www.techtarget.com/whatis/definition/HTTP-Hypertext-Transfer-Protocol -

	---------------------------------------------------

### 3- Why TCP and not UDP ?

HTTP is a "client-server" protocol, which means that when the client wants to communicate with a server, it performs the following steps:

  One: Open a TCP connection, to send a request and receive an answer (establish connection).
  Two: Send an HTTP message (request) to the server.
  Three: Read the answer (response) sent by the server.
  Four: Close or reuse the connection for further requests.

So, why HTTP would use TCP over UDP ?

==> bcuz TCP is realiable, and HTTP requires realiable delivery.
We need TCP connection, to eastablish a connection between the client and server before sending any data, to guarantie transmission realiability and completeness.  

- Resource: https://developer.mozilla.org/en-US/docs/Web/HTTP/Overview -

	---------------------------------------------------

### 4- What is socket (in Computer Network) ?

- We talked about sending and receiving data between the client and the server over the Internet.
	- How ?? 
		==> we already said how (HTTP protocol)
	- Where ??
		==> here comes the utility of using the sockets.

- We already mention, "establishing connection" term, which means creating a bridge where to client and server can send and receive data.
- The "socket" is like a pipe.
- A "socket connecting to the network" is created at each end of the communication(client and server).
==> The socket provides bidirectional FIFO communication facility over the network.

- So the first Socket is created by the client, to ask for eastablishing connection.
- The other Socket is created by the server, to listen for request connection.

- There is two type of sockets, "Datagram Socket" which we are not using and we don't care about, and "Stream Socket" that gonna serve us with the transfer of data.
==> A socket is created using "socket()" system call.

- Resource: https://www.geeksforgeeks.org/socket-in-computer-network/

	---------------------------------------------------
	
### 5- TCP client socket() vs TCP server socket()

1- TCP Client:
	- the client creates a socket using a call to "socket()" fct.
	- the client then establishes the new TCP connection by calling "connect() fct".
	- At this point, the client can freely exchange data using "send()" and "receive()" fcts.

2- TCP Server:
	- the server creates a socket using a call to "socket()" fct.
	- the server bind or link this socket to a port and host using the "bind()" fct.
	- the server puts the socket in a state where it listens for new connections using the "listen()" fct.
	- the server will wait until a client establishes a connection to the server, using the "accept()" fct, and accept() fct returns a new socket, meanwhile the first socket remains listening for new connections.
==> Repeated calls to "accept()" allow the server to handle multiple clients.
	- This new socket created by accept() fct, can be used to exchange data with the client using "send()" and "recv()".

==> Now you are ready to write your first program, for more information about how to create a socket the link in below

- Resources: https://www.gta.ufrj.br/ensino/eel878/sockets/index.html - 

	---------------------------------------------------

### 6- What is Blocking in networking ?

- You probably notice that when you run listen() fct, it sits there until a packet arrives(request).
==> What happened is that the listen() fct call "recvfrom()" fct, and if there was no data, this fct it said "block" (that sleep there) until some data arrives.
Lots of functions blocks, like "accept()", "recv()", which means that our main process sleep and block.
Why ??
==> cuz, when you first create the socket descriptor with "socket()" fct,
	the kernel sets it to blocking.
==> If you don't want a socket to be blocking, you have to make a call to "fcntl()".

	---------------------------------------------------
	
### 7- What is Multiplexing is used for ?

- By setting a socket to non-blocking, you can effectively "poll" the sokcet for information.

==> What is polling anyway ??
"poll" in computing is: check the status of a (device), especially as part of a repeated cycle.

- Generally speaking, "fcntl()" this type of polling is a bad idea,
 a more elegant solution for checking to see if there's data was received and waiting to be read, with the functions of "synchronous I/O Multiplexing".

==> With the multiplexing we can be able to "monitor" a bunch of sockets at once and then handle the ones that have data ready.
==> This way you don't have to continously poll multiple sockets with "fcntl()" to see which are ready to read.

==> There is multiple types of multplexing:
"poll()", "select()", ...

- Resource: 
	==> poll() : 
	==> select():

PS: the diff btw "poll()" and "select()"
select is bitmap the maximum socket that can handle at once are 128 socket.
poll are not limited.
