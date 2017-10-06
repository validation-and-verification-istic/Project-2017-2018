# Project-2017-2018

## Assignement

Each group of students shall choose one of the assignements. Each of these explore an aspect of software testing. It must be implemented in java as a maven project. 
The evaluation will focus on both the quality of the tool and its test suit.


### Assignement 1: Static Analysis

Static analysis consists in processing source code of an application, to extract information from it.

In this assignement, you shall create a tool that use static analysis to detect code smells in Java projects. The tool will explore the structure of the observed project with the help of [Spoon](http://spoon.gforge.inria.fr/).

A [code smell](https://en.wikipedia.org/wiki/Code_smell) is a region of code that exhibits commonly known poor code pattern, resulting in error proneness. Typical examples include huge classes containing too many methods, or methods containing too many nested branches.

You will choose one among the following tasks:
 * High [cyclomatic complexity](https://en.wikipedia.org/wiki/Cyclomatic_complexity): Compute the cyclomatic complexity of each methods in the project.
 * [Duplicated code](https://en.wikipedia.org/wiki/Duplicate_code): Detect cases of code duplication. Bare in mind that code duplication goes beyond text repetition.
 For example (from wikipedia)
```java
int array_a[];
int array_b[];
 
int sum_a = 0;

for (int i = 0; i < 4; i++)
   sum_a += array_a[i];

int average_a = sum_a / 4;
 
int sum_b = 0;

for (int i = 0; i < 4; i++)
   sum_b += array_b[i];

int average_b = sum_b / 4;
```
 
 * Potential Null Pointer Exception: Detect accesses to variables that could be null.
 Example:

```java
String str = null;
if( condition1 )
 str = "fou";
else if ( condition2 )
 str = "barre";
 
int i = str.lenght;//Possible NPE
```

```java
String str = null;
if( condition1 )
 str = "fou";
else if ( condition2 )
 str = "barre";
if (str != null)
 int i = str.lenght;//Fixed
```

Take into account that null test could have been done in some other methods.

 
### Assignement 2: Dynamic Analysis

Unlike Static Analysis, [Dynamic Analysis]() inspects the behaviour or a running program. It can extract useful information such as the code that is being actually executed during testing, that is, the code that is being covered by the test suite. The goal of this assignment is to create a program that computes the code actually covered by the test suite of a given Java project. Your tool should be able to perform at least two of the following analysis:

* Count the number of times each instruction was executed.
* Determine for each branch if all parts has been executed (Branch coverage). 
* Obtain the sequence of method calls performed during testing.
* Record the values used as parameters of constant types for each method.

### Assignment 3: Mutation Testing

[Mutation Testing](https://en.wikipedia.org/wiki/Mutation_testing) is a technique that evaluates the quality of a test suite. A test suite is considered good if it is able to detect bugs. The idea behind Mutation Testing is to create modified versions of the original program, or **mutants** by inserting artificial bugs and then check if the test suite is able to detect those changes. A **mutation** could be simple, for example, replacing **-** by **+** in the context of an arithmetic expression. Other examples could be to replace the boolean expression in a conditional instruction by **false** or replacing a method call by some value. Each type of transformation is usually called a **mutation operator**. A mutation operator can create one or more mutants given the same code.
Your task for this assignment is to create a tool that performs mutation testing on a given Java project. Your tool should incorporate at least 3 of the following mutation operators:

* Replace the boolean expression of a conditional instruction by **false** and, in a second moment by **true**.
* Remove all instructions in the body of a **void** method.
* Replace the body of a boolean method by a single **return true** instruction.
* Perform the following operator substitution in the context of arithmetic expressions:

| Original operator | Replaced by |
|-------------------|-------------|
|        +          |      -      |
|        -          |      +      |
|        *          |      /      |
|        /          |      *      |

* Remove an arbitrary part of a boolean expression. For example: **a && !b** could become **a** or **!b**
* Replace a method call by a predefined value.
* In the presence of an integer constant **x**, replace it by **x+1**, **x-1**, **2*x** and **x/2**.  
* Replace a comparison operator by another given the following possible substitutions:

| Original operator | Replaced by |
|-------------------|-------------|
|        <          |     <=      |
|        >          |     >=      |
|        <=         |      <      |
|        >=         |      >      |

* Replace the right part of an assignment by a predefined value.

You are free to include all the extra operators you want.
A mutation tool can perform the transformations at bytecode level or static source code. This decision is left to you.
[PIT](http://pitest.org/) is a state of the art mutation testing tool for Java programs. In its web site you can find useful information about Mutation Testing and an extended list of possible mutation operators.
Your tool should provide a way to configure the mutation operators to be used in the analysis.


### Improvements

 * UI
 * Additional features
 * ...

### Project to test

 * [commons-codec](https://github.com/apache/commons-codec)
 * [commons-collection](https://github.com/apache/commons-collections)
 * [commons-io](https://github.com/apache/commons-io)
 * [commons-lang](https://github.com/apache/commons-lang)

## Resources

 * [Spoon](http://spoon.gforge.inria.fr/): A library for source code analysis and transformation.
 * [Javassist](http://jboss-javassist.github.io/javassist/): A library for byte code manipulation.
