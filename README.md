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

The goal of this assignement is to create a program that computes the code coverage of a java project's tests.
 * Yes/no
 * Counter
 * Branch
 * Depth
 * Input Domain

### Assignement 3: Mutation Testing

Mutation testing aim at assessing the quality of the test base of a project. To do so it insert error into the project in order to see if the test base detect it. A program transformed is called mutant, if it passes the tests it is a survivor. A transformation is also called a mutation operator. 

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
