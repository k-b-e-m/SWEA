
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
Behavioural pattern

## Intent
Provide a way to access the elements of an aggregate object sequentially without exposing its underlying representation.

## Problem
You want to iterate a collection without worrying about the implementation details of it.

## Solution
Encapsulate iteration itself into an object whose responsibility it is to allow access to each element in the collection.

## Structure
![[Iterator pattern-1.png]]
## Roles
- Collection is some data structure that can be iterated. 
- The Iterator defines the iteration responsibility, and the collection can upon request return an ConcreteIterator that knows how to iterate the specific ConcreteCollection.

## Cost-Benefit
- Benefit
	- It decouples iteration from the collection making client code more resilient to changes to the actual collection used.
	- It supports variations in the iteration as the collection can provide a variety of iterators.
	- The collection interface is slimmer as it does not itself need to provide iteration methods. 
	- You can have several iterators working on the same collection at the same time as each iterator holds its own state information.

- liabilities
	- added complexity in protocol in contrast to traditional iteration.
# Proxy
Behavioural pattern

## Intent
Provide a surrogate or placeholder for another object to control access to it.

## Problem
An object is highly resource demanding and will negatively affect the client’s resource requirements even if the object is not used at all; or we need different types of housekeeping when clients access the object, like access logging (audit trail), access control, or pay-by-access.

## Solution
Define a placeholder object, the Proxy, that acts on behalf of the real object. The proxy can defer loading the real object, control access to it, or in other ways lower resource demands or implement housekeeping tasks.

## Structure
![[Proxy Pattern-1.png]]
## Roles
- A Client only interacts via a Subject interface. '
- The RealSubject is the true object implementing resource-demanding operations (band- width, computation, memory usage, etc.) or operations that need access control (security, pay-by-access, logging, etc.).
- A Proxy implements the Subject interface and provides the relevant access control by holding a reference to the real subject and delegating operations to it.
## Cost-Benefit
- Benefits
	- It strengthens reuse as the housekeeping tasks are separated from the real subject operations.
	- the subject does not need to implement the housekeeping itself; and the proxy can act as proxy for several different types of real subjects.

- Liabilities
	- Does not always have up to date information

# Composite
Structural design pattern

## Intent
Compose objects into tree structures to represent part-whole hierar- chies. Composite lets clients treat individual objects and compositions of objects uniformly.

## Problem
Handling of tree data structures.

## Solution

Define a common interface for composite and atomic components alike. Define composites in terms of a set of children, each either a composite or atomic component. Define composite behavior in terms of aggregating or composing behavior of each child.

## Structure
![[Composite pattern-1.png]]

## Roles
- Component defines a common interface.
- Composite defines a component by means of aggregating other components. 
- Leaf defines a primitive, atomic, component i.e. one that has no substructure.

## Cost-Benefit
 - Benefits
	- It defines a hierarchy of primitive and composite objects.
	- It makes the client interface uniform as it does not need to know if it is a simple or composite component.
	- It is easy to add new kinds of components as they will automatically work with the existing components.
 -  Liabilities
	- The design can become overly general as it is difficult to constrain the types of leafs a composite may contain.
	- The interfaces may method bloat with methods that are irrelevant; for instance an add method in a leaf.
# Null object
Behavioural pattern

## Intent
Define a no-operation object to represent null.

## Problem
The absence of an object, or the absence of behavior, is often represented by a reference being null but it leads to numerous checks to ensure that no method is invoked on null. It is easy to forget such checks.

## Solution
You create a Null Object class whose methods have no behavior, and use an instance of this class instead of using the null type. Thereby there is no need for null checking before invoking methods.

## Structure
![[nullobject pattern-1.png]]

## Roles
- Service defines the interface of some abstraction while 
- ConcreteService is an implementation of it.
- NullObject is an implementation whose methods do nothing.

## Cost-Benefit
 - Benefits
	- It reduces code size and increases reliability because a lot of testing for null is avoided. 
- Liabilities
	- If an interface is not already used it requires additional refactoring to use.

# Observer
Behavioural pattern

## Intent
Define a one-to-many dependency between objects so that when one object changes state, all its dependents are notified and updated automatically.

## Problem
A set of objects needs to be notified in case a common object changes state to ensure system wide consensus and consistency. You want to ensure this consistency in a loosely coupled way.

## Solution
All objects that must be notified (Observers) implements an interface containing an update method. The common object (Subject) maintains a list of all observers and when it changes state, it invokes the update method on each object in the list. Thereby all observing objects are notified of state changes.

## Roles
- Observer specifies the responsibility and interface for being able to be notified.
- Subject is responsible for holding state information, for maintaining a list of all observers, and for invoking the update method on all observers in its list. 
- ConcreteObserver defines concrete behavior for how to react when the subject experiences a state change.

## Cost-Benefit
 - Benefits
	 - Loose coupling between Subject and Observer thus it is easy to add new observers to the system.
	 - Support broadcast communication as it is basically publishing information in a one-to-many relation
 - Liabilities
	- Unexpected/multiple updates: as the coupling is low it is difficult for observers to infer the nature of subject state changes which may lead to the observers updating too often or spuriously.

# Model-View-Controller
Behavioural pattern

## Intent
Define a loosely coupled design to form the architecture of graphical user interfaces having multiple windows and handling user input from mouse, keyboard, or other input sources.

## Problem
A graphical user interface must support multiple windows rendering different visual representations of an underlying set of state-full objects in a consistent way. The user must be able to manipulate the objects’ state using mouse and keyboard.

## Solution
A Model contains the application’s state and notifies all Views when state changes happen. The Views are responsible for rendering the model when notified. User input events are received by a View but forwarded to its associated Controller. The Controller interprets events and makes the appropriate calls to the Model.

## Structure
![[model-view-controller pattern-1.png]]

## Roles
- Model maintains application state and updates all associated Views. 
- View renders the model graphically and delegates user events to the 
-  Controller that in turn is responsible for modifying the mode.

## Cost-Benefit
- Benefits
	- loose coupling between all three roles meaning you can add new graphical renderings or user event processing. 
	- Multiple views/windows are supported. It is possible to change event processing at run-time. 
- Liabilities 
	- unexpected/multiple updates: as the coupling is low it is difficult for views to infer the nature of model state changes which may lead to graphical flickering. 
	- Design complexity is another concern if the development team is untrained.