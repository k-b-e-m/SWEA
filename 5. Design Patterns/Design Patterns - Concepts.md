
# Strategy  pattern
Behavioural pattern
## Intent
**Define a family of business rules or algorithms, encapsulate each one, and make them interchangeable. Strategy lets the algorithm vary independently from clients that use them**
## Problem
**Your product must support variable algorithms or business rules and you want a flexible and reliable way of controlling the variability**
## Solution
**Separate the selection of algortihm from its implementation by expressing the algorithms responsibilities in an interface and let each implementation of the algorithm realize this interface.**
## Structure
![[Attachments/Diagram.svg]]

## Roles
- Strategy
	Specifies the responsibility and interface of the algorithm.

- Concrete Strategy
	Defines concrete behaviour fulfilling the responsibility.
-  Context
	Performs its work for client by delegating to an instance of type strategy

## Cost-Benefit
The benefits are:
	Strategies eliminate conditional statements.
	It is an alternative to Subclassing.
	It facilitates seperate testing if Context and Concretestrategy.
	Strategies may be changed at runtime(If they are stateless).	

The liabilities are: 
	Increased number of objects.
	Clients must be aware of strategies.

# Abstract factory
Creational Pattern
## Intent
Provide an interface for creating families of related or dependent objects without specifying their concrete classes

## Problem
Families of related objects need to instantiated. Product variants need to be consistently configured.

## Solution
Define an abstraction whose responsibility is is to create families of objects. The client delegates object creation to instances of this abstraction.

## Structure
![[Abstract Factory-1.png]]

## Roles
- Abstract Factory
	defines a common interface for object creation.
- ProductA
	Defines the interface of an object
- ConcreteProductA1
	 (Product A in variant 1) required by the client.
- ConcreteFactory1
	Is responsible for creating Products that belong to variant 1 family objects that are consistent with each other.
## Cost-Benefit
- Benefits
- It lowers coupling between client and products as there are no new state- ments in the client to create high coupling. 
- It makes exchanging product families easy by providing the client with different factories. It promotes consistency among products as all instantiation code is within the same class definition that is easy to overview.

- Liabilities
- supporting new kinds of products is difficult: every new product introduced requires all factories to be changed.

# State pattern
Behavioural pattern
## Intent
Allow an object to alter its behavior when its internal state changes.

## Problem
Your product’s behavior varies at run-time depending upon some internal state.

## Solution
Describe the responsibilities of the dynamically varying behavior in an interface and implement the concrete behavior associated with each unique state in an object, the state object, that implements this interface. The context object delegates to its current state object. When internal state changes occur, the current state object reference is changed to refer to the corresponding state object.

## Structure
![[State Pattern-1.png]]

## Roles

- State specifies the responsibilities and interface of the varying behavior associated with a state.
- ConcreteState objects define the specific behavior associated with each specific state. 
- The Context object delegates to its current state object. 
- The state object reference is changed whenever the context changes its internal state.

## Cost-benefit
- Benefits
- State specific behavior is localized as all behavior associated with a specific state is in a single class.
- It makes state transitions explicit as assigning the current state object is the only way to change state. 
- Liabilities
-  increased number of objects and interactions compared to a state machine based upon conditional statements in the context object.

# Facade
Structural pattern
## Intent
Provide a unified interface to a set of interfaces in a subsystem. Facade defines a higher-level interface that makes the subsystem easier to use.

## Problem
The complexity of a subsystem should not be exposed to clients.

## Solution
Define an interface (the facade) that provides simple access to a complex subsystem. Clients that use the facade do not have to access the subsystem objects directly.

## Structure
![[Facade pattern-1.png]]
## Roles
Facade defines the simple interface to a subsystem. Clients only access the subsystem via the Facade.

## Cost-Benefit
- Benefits
- it shields clients from subsystem objects. 
- It promotes weak coupling between the client and the subsystem objects and thus lets you change these more easily without affecting the clients. 

- Liabilities 
- a Facade can bloat with a large set of methods in order for clients to access all aspects of the subsystem.


# Decorator
Structural design pattern
## Intent
Attach additional responsibilities to an object dynamically. Decorators provide a flexible alternative to Subclassing for extending functionality.

## Problem 
You want to add responsibilities and behaviour to individual objects without modifying the class.

## Solution
You create a decorator class that responds to the same interface. The decorator forwards all requests to the decorated object but may provide additional behaviour to certain requests.

## Structure
![[Decorator design pattern-1.png]]

## Roles
**Component** defines the interface of some abstraction while **Concrete-Components** are implementations of it. **Decorator** delegates all method calls to the decorated **Component** object and adds additional behaviour.

## Cost-Benefit
- Benefits
	- Decorators allow adding or removing responsibilities at run-time to objects.
	- They also allow incrementally adding responsibilities in your development process and thus help to keep the number of responsibilities of decorated components low.

- Liabilities
	- Decorators can provide complex behaviour by chaining decorators after one another. A liability is that you end up with lots of little objects that all look alike, this can make understanding decorator chains difficult. 
	- The delegation code for each method in the decorator is a bit tedious to write.
# Adapter
Structural design patter

## Intent
Convert the interface of a class into another interface clients expect. Adapter lets classes work together that couldn’t otherwise because of incompatible interfaces.

## Problem
You have a class with desirable functionality but its interface and/or protocol does not match that of the client needing it.

## Solution
You put an intermediate object, the adapter, between the client and the class with the desired functionality. The adapter conforms to the interface used by the client and delegate actual computation to the adaptee class, potentially performing parameter, protocol, and return value translations in the process.

## Structure
![[adapter pattern-1.png]]

## Roles
- Target encapsulates behavior used by the Client. 
- The Adapter implements the Target role and delegate actual processing to the Adaptee performing parameter and protocol translations in the process.
## Cost-Benefit
- Benefits
	- Adapter lets objects collaborate that otherwise are incompatible.
	- A single adapter can work with many adaptees—that is, all the adaptee’s sub- classes.
# Builder
Creational pattern
## Intent
Separate the construction of a complex object from its representation so that the same construction process can create different representations.

## Problem
You have a single defined construction process but the output format varies.

## Solution
Delegate the construction of each part in the process to a builder object; define a builder object for each output format.

## Structure
![[Builder pattern-1.png]]

## Roles
- Director defines a building process but constructing the particular parts is delegated to a Builder. 
- A set of ConcreteBuilders is responsible to building concrete Products.

## Cost-Benefit
- Benefits
	- It is easy to define new products as you can simply define a new builder. 
	-  The code for construction and representation is isolated, and thus multiple directors can use builders and vice versa. 
	- Compared to other creational patterns (like ABSTRACT FACTORY ) products are not produced in “one shot” but stepwise meaning you have finer control over the construction process.
# Command
Behavioural pattern
## Intent
Encapsulate a request as an object, thereby letting you parameterize clients with different requests, queue or log requests, and support undoable operations.

## Problem
You want to configure objects with behavior/actions at runtime and/or support undo.

## Solution
Instead of defining operations in terms of methods, define them in terms of objects implementing an interface with an execute method. This way requests can be associated to objects dynamically, stored and replayed, etc.

## Structure
![[Command pattern-1.png]]

## Roles
- Invoker is an object, typically user interface related, that may execute a Command, that defines the responsibility of being an executable opera- tion. 
- ConcreteCommand defines the concrete operations that involves the object, Receiver, that the operation is intended to manipulate. 
- The Client creates concrete commands and sets their receivers.

## Cost-Benefit
- Benefits
- Objects that invoke operations are decoupled from those that know how to perform it.
- Commands are first-class objects, and can be manipulated like all other objects. 
- You can assemble commands into composite commands (macros). 
- It is easy to add new commands.
# Iterator
# Proxy
# Composite
# Null object
# Observer
# Model-View-Controller
