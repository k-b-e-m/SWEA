**Uncle Henrik's Clean Code Principles**
# Do the same thing the same way
This affects some different aspects of the code. The simple one is the order in which arguments is put.
For example if having two Math functions, taking to integers as parameters. Where one is the n-root and the other is the pow. One "wrong" way of doing this could be:
``` Java
root(int numberToRoot, int n)
pow(int n, int numberToPower)
```
This is because when one person have been used to for example the root method, and wants to use the pow method, they might mix up the positions of the variables. Therefore always try to make all functions have the arguments in the same order.

Another aspect is closely related to Uncle Bob's "One level of abstraction principle". For example having a method where one part of the method access something within the data structure and the other part access it through an accessor method. This is a problem because of analazibilty, because one would need to know both ways and know that they are algorithmic equal, before they can analyze the actual code.

# Name Boolean Expressions
Naming boolean expressions is smart instead of having to analyze a lot of NOT,AND and OR operations, if made smaller nameable expressions. One can easylier combine them and analyze them.
Another thing here is to name them with "positive" names. So not having a failed, not and so on in the naming. Make the positive one and use the ! in the if statement if the "not" version is needed. This removes most situations where we have not not false, where we have to analyze and think a little more.

# Bail out fast
When making while loops and if statements, it is possible to nest if statements. However this can confuse the reader, because they have to keep track of which boolean expressions is valid and the current "branch" of if statements. Therefore if possible to bail fast, meaning giving a result quick, give it quick instead of working through other code.
Nested if statements is often the same thing as AND operators. A good example is for example a legal statement. Instead of writing:
``` Java
if(exist){
	if(ourUnit){
		if(!tileIsBlocked){
			return unit;
		}
		return null;
	}
	return null;
}
return null;
```
one can write it as
``` Java
if(!exist){
	return null;
}
if(!ourUnit){
	return null;
}
if(tileIsBlocked){
	return null;
}
return unit;
```
This way we bail fast instead of having to remember all current boolean expressions and conditions.


# Arguments in Argument Lists
Arguments of methods should not be named in the method names, And should instead be in the argument list. For example one shouldn't have:

```Java
public double addTaxOf25Pct ( double amount ) ;
public double addTaxOf20Pct ( double amount ) ;
public double addTaxOf12Pct ( double amount ) ;
```
Instead one should make a more general algorithm like:
```Java
public double addTax ( double amount , double taxrate ) ;
```


# ___
**Uncle Bob**

# Naming

- Use Intention-Revealing Names
		If a comment is needed to explain what the variable or class represents, its name is not Intention-revealing

-  Avoid Disinformation
		Avoid names that contains words that means something else. Words like, list, set, ui, hp and so on, since these words mean something else in other contexts. Also using variable names close to each other like 'ListWithAllWordsInCaps' and 'ListWithAllWordsInSmall'. When using the autocomplete, and because these variable names are close to eachother, one might autoextend the wrong variable, and make a bug that is hard to spot, but was easy to avoid.
- Make Meaningful Distinctions
		When having multiple variables or functions which names are made just to satisfy the compiler, the names are usually not meaningful. For example having one variable account1 another account2 is not very meaning full. Is it the first and second account in a list? is 2 a modified version of 1 and so on. Typically numbers, noise words are not good to use in names. 
		Names should be meaningfull and it should be clear, by the name, what the difference is between two variables or functions.
-  Use Pronouncable Names
		Use names that can be pronounced. People talk about code, make them able to say the names without being silly.
-  Use Searchable Names
		Names should be searchable. The longer the name the more searchable. Short names should only be allowed in small scopes. 
			*The length of the name should correspond to the size of the scope*
		Naming constants to static finals, can also help increase search ability for the code.
-  Avoid Encoding
		Do not encode names.
-  Hungarian Notation
		No need to include types in names
- Interfaces and Implementations
		Name the implementations of interfaces something usefull like "ShapeFacotoryImplementation" or "CShapeFactory"
-  Avoid Mental mapping
		Dont be a smart programmer, be a profesional programmer. Clarity is king, and to have the meaning of variables in a mental map is not good. It is not nice to remember that "r" represents the small url. It does not make readable code.
- Class Names
		A class should be a noun and not a verb.
- Method name
		Methods should have verbs, because they do something.
		
- Dont be cute
		Use clear names over entertaining names. Do not name based on jokes or funny humour. Say what you mean. Mean what you say.
- Pick One Word Per Concept
		Have one word for each concept. For example the words fetch,retrieve and get all have similar meanings, however picking just one makes it easier to remember and to use.
- Don't Pun
		Don't use the same word for multiple concepts.
- Use Solution Domain Names
		Use names that explains what the solution is. For example using BFS-Algorithm write BFSToApple. The persons reading your code is programmers and should know what BFS is. This also leads the programmer to go less back and fourth between your solution and the problem description.
- Use Problem Domain Names
		When there are not "Programmer-eese" word for the thing you are coding. Use a word from the problem, at leaest the programmers can look for the meaning through the problem domain.

-  Add Meaningful Context
		When naming variables they give more meaning if they are in a context that gives meaning. For example number can mean a lot of things. But when used in a method called findContactInformation, one can derive that it might be a phone number.
- Don't Add Gratuitous Context
		Dont add so much context that the names consist of mostly context, shorter names are typically better.

# Functions
