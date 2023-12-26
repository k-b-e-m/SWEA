# Direct Input
**Direct input is values or data, provided directly by the testing code, that affect the behaviour of the unit under test (UUT)**

# Indirect input
**Indirect input is values or data, that cannot be provided directly by the testing code, that affects the behaviour of the unit under test**

# Depended on-unit
**A unit in the production code that provides values or behaviour that affect the behaviour of the unit under test**
For example the "AlternatingRateStrategy" in the pay station is depended on a java library behaviour to compute the weekday.


# Test Stub
**A Test stub is a replacement of a real depended-on unit that feeds indirect input, defined by the test code into the unit under test**



# Integration testing
Tests that test that interaction between software units is correct.