
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

# Decorator
# Adapter
# Builder
# Command
# Iterator
# Proxy
# Composite
# Null object
# Observer
# Model-View-Controller
