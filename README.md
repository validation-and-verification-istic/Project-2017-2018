# Project-2017-2018

## Assignement

Each group of students shall choose one of the assignements. Each of these explores an aspect of software testing. It must be implemented in Java as a Maven project. 
The evaluation will focus on both the quality of the tool and its test suite. Systematic controls will be performed by the end of sessions 4 and 7. Final deadline will be on December 22nd 23:59 PM CET. See [Deadlines](#deadlines) section for more details.

### Assignement 1: Static Analysis

Static analysis consists in processing source code of an application, to extract information from it.

In this assignement, you shall create a tool that uses static analysis to detect code smells in Java projects. The tool will explore the structure of the observed project with the help of [Spoon](http://spoon.gforge.inria.fr/).

A [code smell](https://en.wikipedia.org/wiki/Code_smell) is a region of code that exhibits commonly known poor code pattern, resulting in error proneness. Typical examples include huge classes containing too many methods, or methods containing too many nested branches.

You will implement the following:
 * High [cyclomatic complexity](https://en.wikipedia.org/wiki/Cyclomatic_complexity): Compute the cyclomatic complexity of each methods in the project.

And choose one among the following tasks:
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

Unlike Static Analysis, [Dynamic Analysis](https://en.wikipedia.org/wiki/Dynamic_program_analysis) inspects the behaviour of a running program. It can extract useful information such as the code that is being actually executed during testing, that is, the code that is being covered by the test suite. 
The goal of this assignment is to create a program that computes the code actually covered by the test suite of a given Java project. For that you can create a Java agent (more on this [here](http://www.tomsquest.com/blog/2014/01/intro-java-agent-and-bytecode-manipulation/)) to perform the code modification at runtime, and a separated program that computes a report from the information collected.

Your tool should be able to perform at least two of the following analysis:

* Count the number of times each line in the source code was executed.
* Determine for each branch if all parts has been executed (Branch coverage). 
```java
if( a ) fou();
else barre();
```
 In the example above, if `a` is set to `false`, the first line is covered but not the first branch.

* Obtain the sequence of method calls performed during testing.
* Record the values used as parameters of constant types for each method.
```java
String fou(String str, int i) {
 return str.substring(0,i);
}
```
A motivative example could be the method above. If `fou` is only called with positive values, it will cover all method lines, but not detect a problem for negative values. Your tool should track all values used for `i` and `str` and display them.

A good asset for this assignment could be [Javassist](http://jboss-javassist.github.io/javassist/) which is a library for byte code manipulation.

### Assignment 3: Mutation Testing

[Mutation Testing](https://en.wikipedia.org/wiki/Mutation_testing) is a technique that evaluates the quality of a test suite. A test suite is considered good if it is able to detect bugs. The idea behind Mutation Testing is to create modified versions of the original program, or **mutants** by inserting artificial bugs and then check if the test suite is able to detect those changes. A **mutation** could be simple, for example, replacing **-** by **+** in the context of an arithmetic expression. Other examples could be to replace the boolean expression in a conditional instruction by `false` or replacing a method call by some value. Each type of transformation is usually called a **mutation operator**. A mutation operator can create one or more mutants given the same code.
Your task for this assignment is to create a tool that performs mutation testing on a given Java project. Your tool should incorporate at least 3 of the following mutation operators:

* Replace the boolean expression of a conditional instruction by `false` and, in a second moment by `true`.
* Remove all instructions in the body of a `void` method.
* Replace the body of a boolean method by a single `return true` (or `return false`) instruction.
* Perform the following operator substitution in the context of arithmetic expressions:

| Original operator | Replaced by |
|-------------------|-------------|
|        +          |      -      |
|        -          |      +      |
|        *          |      /      |
|        /          |      *      |

* Remove an arbitrary part of a boolean expression. For example: `a && !b` could become `a` or `!b`
* Replace one method call by a predefined value.
```java
int i = fou();
int j = fou();
```
gets transformed into 
```java
int i = 5;
int j = fou();
```

* In the presence of an integer constant `x`, replace it by `x+1`, `x-1`, `2*x` and `x/2`.  
* Replace a comparison operator by another given the following possible substitutions:

| Original operator | Replaced by |
|-------------------|-------------|
|        <          |     >=      |
|        >          |     <=      |
|        <=         |      >      |
|        >=         |      <      |

* Replace the right part of an assignment by a predefined value.

You are free to include all the extra operators you want.
A mutation tool can perform the transformations at bytecode level or static source code. This decision is left to you.
[PIT](http://pitest.org/) is a state of the art mutation testing tool for Java programs. In its web site you can find useful information about Mutation Testing and an extended list of possible mutation operators.
Your tool should provide a way to configure the mutation operators to be used in the analysis.


### Remarks
The assignments described above contain the minimum functionalities excpected, but you are encouraged to add any  functionlities that you find valuable. 
A strong **emphasis** on rigourous testing and other good development practices is expected from you and will be taken into account for the grade.
For the sake of simplicity we expect you to build your project with Maven and junit and you can assume that the same requirements apply for the projects to be analyzed by you.

## Requirements

### Minimal requirements

You are expected to create a public git repository containing at least the following items :
 * a **maven project** containing your code and a **strong junit test suite**
 * a **readme** file specifying how to build your code, how to use the tool on another project, and a section containing the list of targets on which you have tested your tool succesfully.
 * a **report** describing the functionalities of your tool, what problem does it solve, and both the relevence of the solution and its accuracy. A section about how you assessed this accuracy and test your tool overall is expected. You should also mention the problems you have encontered during the developpment and how you solved them. Guidelines concerning this report [can be found here](http://people.rennes.inria.fr/Benoit.Baudry/wp-content/uploads/2013/09/Instructions_for_report.pdf)

### Additional requirements

While meeting the minimal requirements will only give you an average grade, you are expected to put additional thought on tests such as using a continuous integration system ([travis](https://travis-ci.org/) or [jenkins](https://jenkins.io/), or implement additional features (visualization of results, GUI, additional core functionalities).


## Deadlines

At the end of **session 1**, you should have at least decided on the assignement and set up a git repository containing a squeleton Maven project which passes tests.


After **session 4** (November the 22nd 23:59 PM CET for group IL, November the 8th 23:59 PM CET for group IL alternance), you are expected to have implemented some initial functionalities.
Your repository will be cloned and tested at this point. Some analytic tools such as [Pit](http://pitest.org/), [Descartes](https://github.com/STAMP-project/pitest-descartes) and [Cobertura](http://cobertura.github.io/cobertura/) will be used to assess the quality of your test suite.
At the begining of **session 5** we will provide you with feedbacks.


After **session 7** (November the 29th 23:59 PM CET for group IL, December the 5th 23:59 PM CET for group IL alternance), you are expected to have most functionalities running. We will recreate the process described previously, and compare the results.

Feedbacks will be returned to you by the begining of session 8.

Final deadline will be **December the 22nd 23:59 PM CET CET**. 

### Possible target projects

Using real projects as target can be troublesome, so we recommend you to start with the following ones. (We encourage you to go beyond this list)

 * [commons-cli](https://github.com/apache/commons-cli)
 * [commons-codec](https://github.com/apache/commons-codec)
 * [commons-collection](https://github.com/apache/commons-collections)
 * [commons-lang](https://github.com/apache/commons-lang)
 * [commons-math](https://github.com/apache/commons-math)

## Resources

 * [Spoon](http://spoon.gforge.inria.fr/): A library for source code analysis and transformation.
 * [Javassist](http://jboss-javassist.github.io/javassist/): A library for byte code manipulation.
