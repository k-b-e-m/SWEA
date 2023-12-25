# Principles for flexible design
 **From the design patterns book**
## 1. Program to an interface, not an implementation
**I stated a well defined responsibility that covers this behaviour and expressed it in an interface**

### Clients are free to use any service provider class
If one couples something with a concrete class or abstract class, it gives it high coupling to that specific class hierarchy. Limiting the client to only use that kind of class. 
However by using an Interface it enables the client to use multiple classes that just implements that specific interface.

### Interfaces allow more fine-grained behavioural abstractions.
Examples of these are for example the Comparable interface. This is not coupled to concepts, but only to a behavioural aspect of the object, meaning the ability to compare itself with objects of its own class.

### Interfaces express roles
If seeing the different representation and dividing such specific calculations into roles, one ends up with smaller interfaces. This is helpful since some clients might just need one specific behaviour from the Interface, and by using roles, it can gain these.

### Classes define implementation as well as interface
**Imagine that the client does not program to an interface, but to a concrete service class. As a service class defines implementation, there is a risk that the client class will become coupled to its concrete behavior. The obvious example is accidentally accessing public instance variables which creates high coupling. A more subtle coupling may appear if the service
implementation actually deviates from the intended contract as stated by class and method comments. Some examples are for methods to have undocumented side effects, or even have defects. In that case the client code may drift into assuming the side effects, or be coded to circumvent the defective behavior. Now the coupling has become tight between the two as another service implementation cannot be substituted.**

## 2. Favor object composition over class inheritance
**I Instead of implementing the behaviour ourselves I delegated to an object implementing the interface.**

###  Encapsulation
Inheritance breaks the principle of encapsulation since all sub classes have access to its super classes instance variables and methods. This gives high coupling and when a change to a super class is made, all its sub classes would have to be checked and potentially refactored.

When doin programming to a interface, the different clients are only talking through the interface of the class and not withhin the specific class itself. This ensures that they have low coupling and the chance of refactoring is then reduced.

### You can only add responsibilities not remove them

When using inheritance, the sub classes "buy the whole package" meaning that they can only add behaviour, but never remove them.

However when using interfaces one can add only the needed behavioural aspects, and thereby easier full fill its contract on what its responsibilities are.

### Compile time versus run time binding
Class inheritance defines a compile-time coupling between a subclass and its superclass. Once an object of its class has been instantiated its behaviour is defined once and for all throughout its lifetime.

When using composition, the class can change behaviour at runtime, by just changing its delegate for that specific calculation.

### Recurring modification  in the class hierarchy
![[Something something-1.png]]

### Separate testing
When responsibilities are well defined in different interfaces, they become easier to test and will often be tested isolated. If the different behaviours are depended on some units, these units can be replaced by teststubs

### Increased possibility of reuse
Small abstractions is easier to reuse since they often have fewer dependencies.

### Increased number of objects, classes and interfaces.
Because behaviour is split into smaller delegates. The program ends up having more objects, classes and interfaces which the developer needs to keep track of. Here it is important for the developer to have some sort of road map to maintain the overview of the code.

### Delegation requires more boilerplate code
When writing to a interface, one needs to make a lot of boilerplate code, to be able to use it again compared to inheritance.









## 3. Consider what should be variable in your design ( or: Encapsulate the behaviour that varies.)
**I identify some behaviour that is likely to change**



