# The TDD Rhythm
## 1. Quickly add a test
Add a test first to test the case.


## 2. Run all tests and see it fail
Run all tests and see that the new one fails. Sometimes it might pass by standard. Then it is probably a good idea to find out why. Otherwise you can already start step 5.
## 3. Make a little change
Make the production code that makes the new test pass. This should preferably be a small portion of code, because we want to take small steps. Sometimes it can be a bigger portion of code.
## 4. Run all tests and see them all succeed
Run all tests and see them succeed. If they do not succeed go back to step 3. Sometimes the tests could also be wrong!
## 5. Refactor to remove duplication
Now that everything works. Look and the code and check for duplication of code, readability of code and overall apply the principles of clean code.
# Principles of TDD
## Test First
**When should you write your tests? Before you write the code that is to be tested**

This Principle states that one should write the test before the code that is under test. This is because that often one might end up being in such a hurry, that they, would it have been the other way around, wouldn't get to writing the test.

## Automated Tests
**How do you test your software? Write an automated test**
In TDD you run all tests all the time, to ensure new modifications doesn't introduce a defect. Manual tests are too labor intensive, therefore we use automated ones.
## Test List
**What should you test? Before you begin, write a list of all the tests you know you will have to write**

Write a list of which tests you will have to run your program through. This will help you more logically see what the next small step is.

## One Step Test
**Which Test should you pick next from the test list? Pick a test that will teach you something that you are confident you can implement.**

This also heavily relies on taking small steps. For an example you can confidently implement counting money, if you haven't implemented accepting money.

## Fake It
**What is your first implementation once you have a broken test? Return a constant. Once you have your tests running gradually transform it **

We do this to complete test cases from our test list, and not implementing the full algorithm. This is because all production code should be driven by a test. If we implement the full algorithm it is not driven by the tests, which is the principle of test driven development.
Also this ensures that we can keep focus and take small steps.

## Triangulation
**How do you most conservatively drive abstraction with tests? Only when you have two or more examples**

![[Triangulation concept image-1.png]]
Example of triangulaton from other contexts. Here we see that we need multiple instances to get something precise.


This is heavily used for removing fake it code. The principle here is to at least two examples of a test case. For an Example test with both 5 cents and 10 cents in some system.

## Isolated Test
**How should the running of tests affect one another? Not at all.**

Tests should not depend on one another. There for each iteration should write its own test. This makes sure that no ripple effect should appear or be big if it would. This ensures that if a defect is introduced later on, that it will more precisely show what the deficit is about. Good example from the book is:

**"*If you first insert 5 cents, and next want to test the amount of parking time given for 25 cents you must test that the display reads 12 minutes because the total amount entered is 30 cents. This interference between the test cases is relatively easy to overlook here, but in the general case things can get complex and you quickly end up in a ripple effect in the test cases: it is like dominos—if one falls then they all fall. To see this, consider a situation later in development where some developer accidently introduces a defect so the pay station cannot accept 5-cent coins. In the Isolate Test case, then the 5-cent test case would fail and the 25-cent test case would pass. This is a clear indication of what defect has been introduced. In the case where both test cases are expressed in the same test method, however, the whole test method fails. Thus the problems appears worse than it actually is (because apparently both 5 cent and 25 cent entry fails) and also the problem is more difficult to identify (is it a defect in the 5 cent or in the 25 cent validation code?)*"**










## Refactoring
**Refactoring is the process of modifying and restructuring the source code to improve its maintainability and flexibility without affecting the system's external behaviour when executing**


## Evident Data
**How do you represent the intent of data? Include expected and actual results in the test itself, and make their relationship apparent. You are writing tests for the reader, not just the computer**

Here it is a good idea to not have unnamed constants in the test. Put constants in to variables with well defined variable names, use commens for example the "Given When That" ! [[KeyWords  - TDD]] method for commenting.

## Representative Data
**What data do you use fir your tests? Select a small set of data where each element represents a conceptual aspect or a special computational processing.**
Do not select data that is far from the real use of the system. Pick values that are at the borderline when the calculations change. For example pick 5 cents, 10 cents and 15 cents. Where 5 and 10 both can be represented with their separate coin and 15 cents have to be obtained by adding multiple coins together.

## Assert First
**When should you write the asserts? Try writing them first.**
When writing tests, write the assert first, so you clearly knows what this test should have as a result. The thing that is actually to be asserted, can be written after.

## Obvious Implementation
**How do you implement simple operations? Just Implement them**

When implementing simple things like accessor and mutator methods, Just implement them. For all things simple just implement them. This can also sometimes the amount of triangulation code. For example in the "HotStone" project not to add a test case for Findus and Peddersen all the time. And instead implement the obvious of adding both side for example getting their hand, deck etc.

## Evident Tests
**How do we avoud writing defecitve tests? By keeping the testing code evident, readable, and as simple as possible.**

In test the complexity should be kept low. Meaning that the most advanced mechanics of a test should be iterating over and array. Even in this case it is preferred to do it with other means if possible.

## Break
**What do you do when you feel tired and stuck? Take a break**

Programming is hard and demanding. A tired programmer is a bad programmer. Take a break to reduce the number of defects introduced.







# The Test-Driven Process
## Clean code that works
Since each iteration ends with refactoring, this ensures that every little bit of code has been looked at and at least tried to be made clean code, that still works as it should.
## Fast Feedback gives programmer confidence
Because the programmer works in a rhythm that constantly shows that each of the small steps are correct. This gives the programmer confidence and ensures that they can keep focus on each small step. Moreover the tests ensures that the defects in the code can be spotted quickly and therefore is easy to change in the code. This ensures speed of the programming process

## Playing with the interface from the clients side
Since all the code is derived from the test list. Which tries to give situations which the clients/users might put upon the system to solve, all code is therefore made because of a usage from the user. These reduces the amount of unused "cool" feature the programmers might implement.

## Documentation of interface and protocol

The test cases give a kind of Documentation of how the different methods and classes work. However this is not a complete replacement of higher level of documentation.

## No "driver" Code

The typical drivercode that arises from the start of a programs lifecycle, that enables the programmer to test and see what they are building is replacesd by the tests. This is good since the driver code often end up being outdated and unmaintained.


## Structured Programming Process

The principles of the TDD process enables the programmer to use a set of options when writing the code. For an Example the "Fake it", "Triangulation" and so on. This ensures that the programmer can discuss choose and apply these options and doesn't have to go with the "gut feeling" of how to proceed.