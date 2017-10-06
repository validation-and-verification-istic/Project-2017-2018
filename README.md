# Project-2017-2018

## Assignement

Each group of students shall choose one of the assignements. Each of these explore an aspect of software testing. It must be implemented in java as a maven project. 
The evaluation will focus on both the quality of the tool and its test suit.


### Assignement 1: Static Analysis

A code smell is a region of code that exhibit commonly known poor pattern, resulting in error proneness.

The goal of this assignement is to create a program able to detect code smells in java projects. The program will explore the structure of the observed project with the help of [Sppon](http://spoon.gforge.inria.fr/).
 * Large classes or methods
 * High cyclomatic complexity
 * Duplicated code
 * potential NPE

 
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


## Resources

 * [Sppon](http://spoon.gforge.inria.fr/): A library for source code analysis and transformation.
 * [Javassist](http://jboss-javassist.github.io/javassist/): A library for byte code manipulation.
