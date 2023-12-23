
# Source Tree copy
**I simply make a copy of all the source code. In one copy I maintain the Alpha town variant and in the other the Beta town variant. **

## Benefits and liabilities
### Benefits
#### Speed
**It is quick! It is a matter of a single copy operation, modify the test cases
and let it drive the production code changes, and you are ready to ship it to
the customer. This is probably the main reason that it is encountered so often in
practice.**
#### Simple
**The idea is simple and easy to explain to colleagues and new developers.**


#### No implementing in interference
**The two implementations do not interfere with
each other. For instance, if you happen to introduce a defect in the Beta-town
implementation it is guaranteed that it will have no implications on the Alpha-town implementation.**

### Liabilities
#### Leads to multiple maintenance problem
If new features is added to the pay stations, they would have to be added in all the copies of the code.  Same if a defect is detected in one of the pay stations, then it would need to be fixed in all copies of the code.

#### Versions drift a part
When multiple programmers work with multiple source files. Over time they will drift a part, and one might end up maintaining 8 different applications instead of 8 different variants of the same variant.

# Parametric
**I introduce a parameter that defines the town the software is
running in: either Alpha town or Beta town. I only have one copy of the production code but at appropriate places (in my concrete case: in the rate calculation
variability point) the code branches on this parameter to give the behaviour required.**

## Benefits and Liabilities
### Benefits
#### Simple
**Conditionals are easy to understand and often one of the first language
constructs introduced to new learners of programming. Thus the parametric
idea is easy to describe to other developers.**

#### Avoids the  multiple maintenance program
**There is only one code base to maintain
for both Alpha town and Beta town. Thus a defect in common behaviour can be
fixed once and for all. As argued above most of the pay station’s production
code is identical for both towns and this will therefore make bug fixing less
expensive and less prone to errors. Also new features for the pay station that
both towns can benefit from is also less costly to develop as only one production
code base is affected by added code and new tests
**


### Liabilities
#### Reliability concerns
**The new requirement is handled by change by modification ([[Keywords - Variability management]]) that has a risk of introducing new defects**

#### Analyzability concerns
**As more and more requirements are handled by parameter switching, the production code becomes less easy to analyse**

#### Responsibility Erosion
**The pay station has, without much notice, been given an extra responsibility.**


# Polymorphic
**I can subclass the PayStationImpl and override a method
that calculates the rate.**

![[Polymorphic proposal example-1.png]]

## Benefits and liabilities
### Benefits
#### Avoid the multiple maintenance problem 
**I only have one code base which is good property as already argued**
explained in the Parametric proposal.

#### Reliability concern
**The production code has once and for all been prepared for any new rate policy to be required earlier**
#### Code analyzability
**This proposal does not suffer from code bloat, you have less code to read  to understand a variant.**


### Liabilities
#### Increased number of classes
**Every rate policy will now introduce a new subclass.**

#### Inheritance relation spent on single type of variation
**I cannot use the inheritance relation to handle other types of variations**

#### Reuse across variants difficult
**It turns out to be cumbersome to reuse the algorithm defined by one variant in another.**

#### Compile-time binding
**The binding between the particular rate policy and the pay station id defined at compile time.**

# Compositional
**I can describe the variable behaviour, rate calculation, in an interfacec and have classes implementing each concrete rate calculation policy. I then let the pay station call such a rate calculation object instead of performing the calculations itself.**

![[Compositinal delgation-1.png]]
Example of using compositional design to calculate rate.

In the compositional version of variability management. The different responsibilities is divided into a set of objects that will then collaborate and together give the desired behaviour. Meaning that the compositional management of variability is a heavy user of delegation. [[Keywords - Variability management]].

Compositional design heavily relies on the principle of *let someone else do the dirty job!*"


## Benefits and liabilities of compositional design
*all these is in perspective to the pay station rate strategy example*
### Benefits
#### Reliability
**The pay station has been refactored once and for all with respect to rate calculations, and new rate calculations can be handled only by adding more classes.**

#### Run-time binding
**The binding between the pay station and its associate rate calculation can be changed at runtime**'
 
 #### Separation of responsibilities
 **Responsibilities  are clearly separated  and assigned rate calculation can be changed at run-time** 
#### Separation of testing
**As the responsibilities have been separated I can actually test rate calculations and core pay station functionality independently**

#### Variant selection is localised
**The code that decides what particular variant  of rate calculation to use is in one spot only**

#### Combinatorial
**We can introduce other types of variability without interfering with rate calculations variability**

### Liabilities
#### Increased number of classes and interfaces
**The number of classes and interfaces has grown in comparison to the original design**

#### Clients must be aware of strategies
**The selection of which rate policy to use is no longer in the  
pay station but still someone has to make this decision. Variant selection is moved to the client objects.**


## The compositional process
Identify some behaviour that varies.
State a responsibility that covers the variable behaviour
Delegate the behaviour
This is called the [[3-1-2 process]], which is further explained here.

