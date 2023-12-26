# Classifying Test stubs

## Test  Stub
**A double whose purpose it is to feed indirect input, defined by the test case, into the UUT**

## Test spy
**A double whose purpose it is to record the UUT's indirect output for later verification by test case**

Mostly used to ensure that a series of commands appear in the correct order.
For example a robot with some motors. Here the motors could be replaced by a spy can record the commands, and then verify their order later.

## Mock object
**A double, created and programmed dynamically by a mock library, that may both serve as a stub and a spy**

![[Mock object-1.png]]

## Fake Object
**A double whose purpose is to be a high performance replacement for a slow or expensive DOU**

Used for replacing expensive and slow DOU, this could for example be a database.



