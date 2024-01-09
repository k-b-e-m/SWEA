# Basic Concepts
## Distributed System
Traditionally distributed system have been designed with two purposes in mind.
To Increase computational power, that is, to allow complex calculations to be performed faster by utilizing more than a single computer.
To share large amounts of data, that is, by storing data on a single central computer, a large number of other computers and thus users can access and modify common information.

## Client-server architecture
Two independent components need to communicate with each other, even if running on different computers or different processes. 
Client
	Requests information from the services from a server.
	Needs to know how to connect with the server using id or address to server.
	Optimized for application tasks

Server
	Responds requests and processes client requests.
	Do not know the clients id or address before the interaction.
	Optimized for serving multiple clients

## Issues of Distributed systems

- Remote Objects do not share address space. Thus, references to local objects on my machine passed to a remote object on a remote machine are meaningless. We can therefore not pass references to strings, objects etc through the system.
- Networks only transport bits and bytes with no understanding of classes, interfaces, or types which are fundamental structuring mechanisms in modern programming languages. In essence, a network is similar to a file system: just as a program’s internal state needs to be converted to allow writing and reading from a disk—the internal state must be converted to allow sending it to a remote object. 
- Remote objects may execute on different computing architectures, different CPUs and instruction sets. The problem is that different processors layout bits differently for for instance integers.
- Networks are slow. Invoking a method on a remote object is between 10-250 times slower than if the object is within the same java virtual machine.'
- Networks fail. This fundemental property means methods called on remote objects may never return.
- Remote computers may fail, thus the remote object we need to communicate with may simply not be executing.
- Networks are unsafe. Data transferred over networks can be picked up by computers and people that we are not aware of, that we can not trust.
- Remote objects execeute concurrently. This we face all the troubles of concurrent programming at the very same moment we program for distributed systems.
- If too many clients invoke methods on a server, it will become overloaded and respond slowly or even crash - typically because memory is exhausted.

## Request - Reply
The request-reply protocol simulates a synchronous call between client and server objects by pairwise exchange of messages.
one forming the request message form the client to server, 
and the second forming the reply message from the server back to the client. The client sends the request message, and waits/blocks until the reply message has been received.
![[Reply request protocol-1.png]]

## Marshalling
[[Distributions and Broker - Keywords]]
Different formats for mashalling
Binary
	- Fast, but reliant on the CPUs encoding, which may vary from system to system. Still used in for example online gaming.

Extensible Markup Language (XML)
	![[Example of XML-1.png]]
	Here is an example of XML
	The advantages of XML is that it is well known, standardized and supported by a lot of tools and software libraries. However its disadvantages is that it is verbose, which makes it harder to read and requires a lot of requirements of the hardware in terms of bandwidth to carry the large amounts of text.

JavaScript Object Notation (JSON)
	![[Example of JSON-1.png]]Here is an example of JSON

## Proxy
The proxy pattern [[proxyPatternPensum.pdf]]

## Name Services
A Name Service is a class, which consists of a bunch of maps, from some kind of unique id, For example UUID, to communicate about specific objects.

*Name service is the role of a storage that can bind object names or identities to the real objects. Thereby we can transmit object identities instead of object references between clients and servers and use the name service to resolve which actual object to communicate with.*


# Broker part one
## The Problem
Distributed systems consists of objects that are located on different computers. We want to program a object-oriented model that supports calling methods on clients with remote objects. All method calls for the clients should act as closely as  possible to normal method calls. Meaning they should not include low level distributed system calls like  send() and recieve() methods.

## The broker pattern 
### Broker in short
![[Architecture Pattern in short-1.png]]
### Structure
![[Broker Structure-1.png]]

### Protocol

![[Broker Client side dynamics-1.png]]
![[Broker server side dynamics-1.png]]

### Roles
#### Client Proxy
- Proxy for the remote servant object, implements the same interface as the servant. Acts like a placeholder for the real object which is on the servant server side.
- Translates every method invocation into invocations of the associated Requestor's request() method.
#### Requestor
- Performs marshalling of object identity, method name and arguments into a byte array.
- Invokes the ClientRequestHandler's send() method
- Demarshalls returned byte array into  return values.
- Creates client side exceptions in case of failures detected at the server side or during network transmission
#### ClientRequestHandler
- Perform all inter process communication send/receive of data onbehalf of the client side, interacting with the server side's ServerRequestHandler
#### ServerRequestHandler
- Performs all inter process communication on behalf of the server side interacting with the client side's ClientRequestHandler.
- Contains the event loop thread that awaits incoming requests from the network
- Upon receiving a message, calls the Invoker's handleRequest method with the received byte array. Sends the reply back to the client side.
#### Invoker
- Performs demarshalling of incoming byte array
- Determines servant object, method and arguments and calls the given method in the identified Servant object.
- Performs Marshalling of the return value from the servant object into a reply byte array, or in case of server side exceptions or other failure conditions, return error replies allowing the Requestor to throw appropriate exceptions.
#### Servant
- Domain object with the domain implementation on the server side. The "Actual" program/software.

### Limitations
- The structure is pure Client-Serveer, that is, the server can never invoke a method on an object on a client. It is always the client that makes a call.
- The location and identity of the server object must be known to the client as my description above did not include any name service.
- The arguments to any method call are pass-by-value. as they must be able to marshall and demarshall to produce identical results on both client and server. Pass-by-reference cannot be handled as there is no name service to resolve remote references.

## Marshalling Robustness
**Key Point: Include format Version Identity**
	*Always include version identity in the marshalling format*
Meaning always let older versions of Marshall still work for the server.


# Implementation of the Broker

## Domain Layer
 At the domain layer we need a servant and ClientProxy  both implementing the the interface which is to be distributed.
## Client Side

### ClientProxy

#### Example of ClientProxy Code
![[Client proxy code-1.png]]
 The client and the server will communicate on which metod to invoke using a unique string froe each operation. Here we see that there are some predefined "public static final String ..." in the class called OperationNames.

### Requestor
The requestor's responsibility is to marshall the method call, delegate the client request handler to send/recieve and demarshall the response.
 Here we can use different requester for the hotStone project we used:
 a JSON requestor.
![[Example of a requestor-1.png]]

Here wer also see that we have the **Request- and ReplyObject** These objects are just to package all the information into one class. These are for convenience and only consists of accessor methods and stores information. They make the Gson marsshalling library easier.

### ClientRequestHandler

## Server Side
### ServerRequestHandler

![[ServerRequestHandler code-1.png]]

### Invoker

Example code of the GameInvoker from the hotStone Project:
``` Java
@Override  
public String handleRequest(String request) {  
    RequestObject requestObject = gson.fromJson(request, RequestObject.class);  
    JsonArray array = JsonParser.parseString(requestObject.getPayload()).getAsJsonArray();  
    ReplyObject reply=null; //To initialize  
  
    String objectId = requestObject.getObjectId();  
  
  
  
    if(requestObject.getOperationName().split("_")[0].equals(GAME_PREFIX)) {  
        switch (requestObject.getOperationName()) {  
            case GAME_GET_TURN_NUMBER -> {  
                int uid = game.getTurnNumber();  
                reply = new ReplyObject(HttpServletResponse.SC_OK, gson.toJson(uid));  
            }  
            case GAME_GET_PLAYER_IN_TURN -> {  
                Player uid = game.getPlayerInTurn();  
                reply = new ReplyObject(HttpServletResponse.SC_OK, gson.toJson(uid));  
            }  
            case GAME_GET_WINNER -> {  
                Player uid = game.getWinner();  
                reply = new ReplyObject(HttpServletResponse.SC_OK, gson.toJson(uid));  
            }  
            case GAME_GET_DECK_SIZE -> {  
                Player player = gson.fromJson(array.get(0), Player.class);  
                int uid = game.getDeckSize(player);  
                reply = new ReplyObject(HttpServletResponse.SC_OK, gson.toJson(uid));  
            }  
  
            case GAME_GET_FIELD_SIZE -> {  
                Player player = gson.fromJson(array.get(0), Player.class);  
                int uid = game.getFieldSize(player);  
                reply = new ReplyObject(HttpServletResponse.SC_OK, gson.toJson(uid));  
            }  
  
            case GAME_GET_HAND_SIZE -> {  
                Player player = gson.fromJson(array.get(0), Player.class);  
                int uid = game.getHandSize(player);  
                reply = new ReplyObject(HttpServletResponse.SC_OK, gson.toJson(uid));  
            }  
  
            case GAME_END_OF_TURN -> {  
                game.endTurn();  
                reply = new ReplyObject(HttpServletResponse.SC_OK, gson.toJson(null));  
            }
///
///
//..
```


## TDD on Distributed Systems
When Developing a Distributed System using TDD we heavily use Spy

To helo devolop the ClientProxy, we use a RequestorSpy.
Further More in the Invokers, we can have FakeRequestHandlers, such as databases, cards, heros and so on.
![[4.7 using Henrik Broker Library-1.png]]
4 Meszaros, Gerard, “xUnit Test Patterns - Refactoring Test Code”, Addison Wesley, 2007.
5 https://bintray.com/henrikbaerbak/maven/broker 
6 https://www.rabbitmq.com/
# Broker part two
## Gamelobby
![[Game lobby dynamics-1.png]]

We here have 3 different roles.

### Gamelobby
- Singleton object, representing the entry point for creating and joining games.
### FutureGame
- A Future, allowing the state of the game (Available or not) to be queried, and once both players have joined, return the game object itself. 
- Provides an accessor method getJoinToken() to retrieve the join token that the second user must provide.
### Game
- The actual game domain role.


## Dynamics of broker II
![[Dynamicsc of broker 2-1.png]]
### Invoker
- Performs demarshalling of incoming byte array. 
- Determines servant object, methods, and arguments (some of which may be object IDs in which case the servant reference must be fetched from the Name Service), and calls the given method in the identified Servant object. 
- Performs marshalling of the return value from the Servant ob- ject into a reply byte array, or in case of server side exceptions or other failure conditions, return error replies allowing the Requestor to throw appropriate exceptions. 
- When servants create new objects, store their IDs in the Name Service and return their ID instead.
### Requestor
-  Performs marshalling of object identity, method name and ar- guments into a byte array. 
- Invokes the ClientRequestHandler’s send() method. 
- Demarshalls returned byte array into return value(s). If returned value is an object ID of a server created object, create a Client- Proxy with the given object ID and return that. 
- Creates client side exceptions in case of failures detected at the server side or during network transmission.
### Name Service
-  A server side storage that maps objectId’s to objects 
- Allows adding, fetching, and deleting entries in the storage

# HTTP
Powers the World Wide Web.
Standard for the Request-reply protocol for web browsers and web servers.

Format of a request HTTP:
- A request line, that specifies the HTTP verb, the wanted resource, and the version of the HTTP protocol.
- Request header fields, which are key-value pairs defined by the HTTP protocol.
- An empty Line
- An Optional message body

 ![[A HTTP request-1.png]]
 An HTTP request

![[HTTP reply-1.png]]
HTTP reply

Reply HTTP Format
- A single status line which includes the status code and status message
- Response header fields, again a set of well-defined key-value pairs on multiple lines
- An empty line
- The (optional) message body, that is the contents of the requested resource.


![[HTTP actions-1.png]]

**All verbs, except POST, are idempotent which means that executing them several times has the same effect as only executing it once. If you send one or ten identical PUT requests to the server, the outcome is the same, namely that the named resource is updated. The POST is different, as sending two POST requests will create two resources, etc.**

Status Codes for HTTP

- 200 OK
- 201 Created
- 404 Not Found
- 501 Not Implemented
- 406 Not Acceptable

# Rest (Representational State Transfer)
Rest in an architectural style. 

## Demise of Broker Architectures
The Broker pattern were big around the 90's. However because a lot of programmer made high coupling between the server and client objects, it was seen as if the Broker pattern were broken, and not that the programmers did something wrong. - Opinion of Henrik Bærbak

Another Issue with the Broker pattern is that it requirres the user to work with a stateless server. 
GeeksForGeeks on stateless Servers:
*As the name suggests, the stateless server has no state with regard to the user’s information. It means when the user access any web resource, the server does not keep a track of the user’s identity or actions performed on the page. So every time, the user has to prove the identity to gain access.

*Let’s understand it better in contrast with the stateful server. Stateful servers store users’ state information in the form of sessions. It stores information like profile, preference, user’s action and gives personalized experience on next visit. The user does not need credentials every time during the valid session.*  

*While stateless server treats each request as independent and demand user credentials. It requires no knowledge of previous interactions and stores no session information. So, there’s no difference between previous, current, and next requests.**

Otherwise if the server shuts down, all data/actions would be lost.







## REST
There is five central principles of REST
- The central concept is the resource which is defined as any information that can be named.
- A resource is identified by a resource identifyer
- You transfer a representation of data in a format mathcing one of the standard media types.
- All interactions are stateless, i.e. every request must contain all the information necessary for processing it.
- Interactions are between clients and servers, the essential difference between the two is that a client initiates communication by making a request, whereas a server listens to connections and responds to requests in order to supply access to its services.


## Levels of Rest
- Level 0: URI Tunneling
	HTTP is used with a well supported IPC layer., like spark and unirest. 
- Level 1: HTTP Verbs
	Systems start obeying the HTTP requirements. You can use the HTTP verbs to modify and retrieve the content.
- level 2: Hypermedia

## Similarities between Broker and REST.
- The Request-Reply protocol is central in both styles. In >Broker, we may have to code it directly in the Request Handlers if we use sockets, while the HTTP already implements it.
- The need for Marshalling of data contents. In Broker, we again coded it in the Requestor/Invoker pair, while HTTP relies on media types.
- The need for Name services. In Broker, we used the DNS systems to get the IP adress of the server, while we used an+ internal implementation for getting a servant object associated with a given object id. REST, on the other hand, encodes everything into the URI: both the server identity as well as the resource identity.
- The Proxy is only an issue for object-oriented designs.ø
##  Testability and TDD of REST designs
Two options exists
- Use Integration testing techniques: Spawn a REST server in the JUnit fixture, send HTTP requests as part of the test cases, and verify the return HTTP responses. Downside: Brittle tests that may be slow.
- Use the Facade patter to encapsulate the REST paradigm using 3-1-2. Downside: There is more code to produce.