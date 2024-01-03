# What are objects?
When talking about what objects are there are typically 3 ways to look at it

## The Language-Centric Perspective
Typical definition of objects in this perspective is:
"*An object is a program construction that has data (that is information) associated with it and that can perform certain actions.*"

Here the emphasis is on the fields and methods of the class that the object belongs in.
This is inherently a compile-time or static view.
It speaks of what we can see in our editor.

## The Model-Centric perspective
Typical definition:
*Java objects model objects from a problem domain*

Here the objects are used as a form of model/simulation of the real world counter part. For example having an Account and an owner as a class.

This perspective leads to a strong focus on what the relations are between the elements of the model.


## The Responsibility-Centric perspective
Typical definition:

*The best way to think about what object is, is to think of it as something with responsibilities*

Here meaning that compared to the two previous perspectives, this perspective is not focused on the real world counterpart or their relations, but more about the responsibilities. Each object represents a certain role with a certain or very few responsibilities

When using this perspective, one ends up having a lot of different individual objects working together on something greater. For example one object might do the calculation for a specific thing, and another might be responsible for "telling" the object to do that calculation.

This perspective is the one that compositional design heavily relies on

# Roles, Responsibility and behaviour
## Behaviour
This is some observable actions. In code it is typically the methods performed, the algorithms. 

## Responsibility
When having a responsability it is more about having a contract. When an object is responsible of something, it does not matter how they do it, but that they do it. How they do it depends on the behaviour of the object taking upon the responsibility

To define responsibilities it cannot be too specific or to vague. A good way to find the responsibility is by using CRC cards [[Compositional Designs - Keywords]].  
The closest langauge construct to the responsibilities are the interfaces. This makes sense since the interface can define some method names, expecting some behaviour to solve a problem, but not define how they should perform. For example ManaStrategy interface in hotstone, have the responsibility to calculate the mana, but not the behaviour of how to do it.

## Role

**Key Point**
*A role can be played by many different types of objects. An object can perform many different roles withing a system*

Roles is to take upon different responsibilities. For example a teacher, Student, Nurse, Doctor. One does not know the specific person taking the role, but they do however know their responsibilities. For example a student much listen, a teacher must teach and so on. One person can take upon multiple roles.
In programming this corresponds with objects implementing interfaces. For example implementing Comparable, Serializable and other Interfaces. Here the object has a role of being sortable from the Comparable but also able to save it as a file on the pc, form the Serializable. This leads to that other objects can collaborate with the object by using these roles without knowing the specific object.

Roles does not have any direct counterpart in a programming language. The closest ones are the interface. To fully use Interfaces as roles,  is the job of the programmer.

## Protocol

Protocol is the way the different roles are expected to respond with eachother. For example **Context** initiates execution while **ConcreteStrategy** reactivly responds when requested.
For Example the paystation requests a calculation from the ratestrategy and the the ratestrategy responds with an answer.
This is typiccally shown with UML sequence diagrams.
![[Example of UML Sequence Diagram-1.png]]
**UML Sequence Diagram example**


