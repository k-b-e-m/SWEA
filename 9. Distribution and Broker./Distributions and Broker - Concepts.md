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

