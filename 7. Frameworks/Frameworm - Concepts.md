# Framework Definitions

-  framework is: a) a reusable design of an application or subsystem b) repre- sented by a set of abstract classes and the way objects in these classes collabo- rate (Fraser et al. 1997).
 -  framework is a set of classes that embodies an abstract design for solutions to a family of related problems (Johnson and Foote 1988).
 -  framework is a set of cooperating classes that make up a reusable design for a specic class of software (Gamma et al. 1995, p. 26).
 -  framework is the skeleton of an application that can be customized by an application developer (Fayad et al. 1999a, p. 3).
 -  framework denes a high-level language with which applications within a domain are created through specialization (Pree 1999, p. 379).
 -  framework is an architectural pattern that provides an extensible template for applications within a domain (Booch et al. 1999, p. 383).

# Framework Characteristics
## Skeleton / design / high-level language / template
that is, the framework delivers application behavior at a high level of abstraction. This is much in line with the general definition of a framework as a basic conceptual structure.

## Application / class of software / within a domain
that is, a framework provides behavior in a well-defined domain.

## Cooperating / collaborating classes:
that is, a framework defines the protocol between a set of well-defined components/objects. To use the framework you have to understand these interaction patterns and must program in accordance with them.

## Customize / abstract classes / reusable / specialize
that is, a framework is flexible so that you can tailor it to a concrete context, as long as this context lies within the domain of the framework.

## Classes/ Implementation / skeleton
that is, a framework is reuse of working code as well as reuse of design.

# Types of users and developers

There are three types of users:

-  framework developers
		Designs and codes the framework.
- application developers
		customises the framework to specific needs. Users of the framework.
- users
		users of the application that has used the framework.
		
## Things to consider when application developers use the framework
 - the framework’s domain must be sufficiently close to the domain/problem that the application developers are trying to address. 
 - the framework must be sufficiently flexible so the application developers can adopt it to the specific context. If the framework is lacking ways to customize it in places where the application developer needs to adjust the provided functionality then the framework is of course less suited or inappropriate for the problem at hand. 
 - the framework must deliver a design, functionality, and domain knowledge that otherwise is very expensive to acquire. This speaks in favor of frameworks of some complexity and size. 
 - the framework implementation must be reliable. Reusing a framework that is full of defects is definitely only “reused” once.


# Frozen and Hot spots
**Key point**
*A framework is a closed, blackbox, software component in which the source code must not be altered even if it is accessible. Customization must only take place through providing behavior in the hot spots by those mechanisms laid out by the framework developers.*

# Defining Variability points
**Key point  Frameworks must use dependency injection**
*Framework objects cannot themselves instantiate objects that define variability points, these have to be instantiated by the application code and injected into the framework.*

A more hands-on rule is that framework code must never contain a new statement on classes that have hot spot methods defined.

Frameworks present a range of possibilities for defining the hot spot objects. 
-  Existing concrete classes. The framework comes along with a (large) number of predefined classes and your job is to compose these into something sensible. AWT and Swing are examples where you compose new graphical user interfaces from predefined components. 
- Subclassing an abstract class: the framework contains abstract classes so most of a high quality implementation is already given, leaving you with the task of filling out the last details. 
-  Implementing an interface: the framework contains an interface, giving the application developer the opportunity to exercise full control over the hot spots.

**Key Point: Frameworks should support the spectrum from no imple- mentation (interface) over partial (abstract) to full (concrete) implementation for variability points**
*A framework provides the optimal range of possibilities for the application devel- oper if all variability points are declared in interfaces, if these interfaces are par- tially implemented by abstract classes providing “common case” behavior, and if a set of concrete classes for common usages is provided.*

# Inversion of Control
A feature of frameworks is that they define the flow of control in the application. The framework defines in which order the different collaborating classes should interact and how. This is called the principle of inversion of control. The framework defines the flow of control, not you. Some also call it the hollywood principle, "Don't call us, well call you."

For example when we are using a library like java.Math. Our code is in control. When a math calculation is needed we briefly give the control to the math library to do the math calculations.
However with Inversion of control, The framework is in control. And briefly gives our code the control when needed. Thereby the framework calls us, we do not call it.


# Framework Composition
![[Framework composition-1.png]]
Use composition and the 3-1-2 method when building frameworks instead of abstract classes and inheritance.


# Software Reuse
**Key Point: Framework reuse is reuse of both design and code**
*A framework is a tangible unit of software, thus it is code reuse. However, due to the inversion of control property, it also defines the flow of control, object protocols, and clearly defines the variability points, and thus bundles a quality design as well.*



# Summary of what a framework is
A framework is a reusable design together with implementation for a specific class of applications. A framework consists of Frozen and Hot spot