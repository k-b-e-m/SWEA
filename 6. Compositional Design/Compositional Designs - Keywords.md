# Object-orientation(Model)
**A program execution is regarded as a physical model simulating the behavior of either a real or imaginary part of the world.**

# Object-orientation (Responsibility)
**An object-oriented program is structured as a community of interacting agents called objects. Each object has a role to play. Each object provides a service or performs an action that is used by other members of the community**


# Behaviour
**Acting in a particular and observable way.**

# Responsibility
**The state of being accountable and dependable to answer a request**

# CRC cards
**C**lass - what class the card shows
**R**esponsibilities - Which responsibilities they have
**C**ollaborators - which classes they collaborate with
Example:
![[CRC paystation-1.png]]

# Role(General)
**A function or part performed especially in a particular operation or process**
# Role(Software)
**A set of responsibilities associated protocols**
# Protocol
**A convention detailing the sequence of interactions or actions expected by a set of roles**

# Interface Segregation Principle
**In the field of software engineering, the interface segregation principle (ISP) states that no code should be forced to depend on methods it does not use. ISP splits interfaces that are very large into smaller and more specfic ones so that clients will only have to know about the methods that are of interest to them. Such shrunken interfaces are also called role interfaces.**

- **KEY POINT**
Roles should not cover too many responsibilities but stay small and cohesive. Complex roles may then be defined in terms of simpler ones.

# Role Interface
**A role interface is defined by looking at a specific interaction between suplliers and consumers. A supplier component will usually implement several role interfaces, one for each of these patterns of interaction.**

# Private Interface
**Provide a mechanism that allows specific classes to use a non-public subset of a class interface without inadvertently increasing the visibility if any hidden member variables or member functions**
