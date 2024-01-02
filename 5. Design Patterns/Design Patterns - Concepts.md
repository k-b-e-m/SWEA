
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
## Intent


# State pattern
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
