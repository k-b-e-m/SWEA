# Whitebox- and blackbox-testing

## Blackbox
**The unit under test (UUT) is treated as a black box. The only knowledge we have to guide our testing effort is the specification of the UUT and a general knowledge of common programming techniques, algorithms constructs, and common mistakes made by programmers.**

## WhiteBox
**The full implementation of the unit under test is known, so the actual code can be inspected in order to generate test cases.**

# Testing strategies
## No Testing
Mostly used for simple methods like accessor methods. Here the methods is so simple that a test will be longer than the method. There would therefore be a higher risk of the fail being in the test code, rather than the production code.

## Explorative testing
These tests are tests based on a gut feeling. these tests is what is used for the TDD process. These tests are really good for an experienced TDD developer and testers.

## Systematic testing

Here you follow methods for generating test cases. Here a lot of the time is spend on analysing the problem. However, although these tests are the most time consuming, they are also the most reliant tests to find defects in '
software.

# Equivalence class partitioning


This concept talks about dividing possible inputs into equivelent classes. For an example testing the method Math.abs from java. All positive numbers are in the same class and all negative numbers are in the same class. For this method the table would then look like:

|   Condition   | Invalid ECs     |   Valid ECs   |
|:-----|:-----|:-----|
|   absolute value of x   |  -    |  x>0[1], x$\leq$ 0 [2]|

Keep in mind that in this case there are no illegal ECs, however some methods might have some input which is not allowed, and these would thereby called invalid EC's.
## Soundness of ECs
**All ECs have two properties to be sound**
1. **Coverage** all possible inputs is covered within at least one EC
2. **Representation** If a defect is demonstrated on a particular member of an EC, then the same defect is assumed to be demonstrated by any other member of the class.

## Finding Equivalence classes
There are three types of conditions
1. **Range**
		If a condition is specified as  a range of values, select one valid EC that covers the allowed range, and two invalid ECs, one above and one below the end of the range.
2. **Set**
		If a condition is specified as a set of values, then define tan EC for each value in the set and one EC containing all values outside the set.
3. **Boolean**
		If a condition is specified as a "must be" condition then define one EC for the condition being true and one EC for the condition being false.


## Generating the test cases
When all the ECs are found, the process of generating test cases can be done by the following heuristic:
1. Until all valid ECs have been covered, define a test case whose covers as many incovered valid test cases as possible.
2. Untill all invalid ECs have been covered, make a test case where there only exists one invalid EC.

## The process of EC
1. Review the requirements for the UUT and identify conditions and use the heuristics to find the ECs for each condition. ECs are best written down in an equivalence class table.
2. Review the produced ECs and consider carefully the representation property of the elements in each EC.  Check that all elements are Representative in the EC.
3. review to verify the coverage property is fulfilled.
4. Generate test cases from the ECs. You can often use Myers heuristics for combination to generate a minimal set of test cases. Test cases are best documented using a test case table.


# Boundary Analysis
A common mistake in programming is the "off by one case" Where the value on the boundary is not acting correctly. For example using <= instead of < in Java and so on.
The analysis here is simply just to identify the boundary variables to spot these "off by one" errors.
