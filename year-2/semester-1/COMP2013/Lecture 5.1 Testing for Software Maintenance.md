
This year is about more advanced principles of testing, with more complicated forms of it, and an understanding of how testing relates to maintenance. It also gives practical experience with CI/CD pipelines.

> All about: **Understanding the links between regression testing, TDD, refactoring and legacy code.**

Unit testing is done by starting the test with what it needs (preconditions) - e.g. instantiate objects, mock data. Then, perform the action and get the result. Finally, assert that the result is as expected.

TDD is done by writing the stub method if required, and writing a test that should fail. Then, create the simplest implementation of a method to make the test pass. Finally, go back to the implementation and refactor it until it is acceptable.

## Testing in DevOps

The aims of Ops are to create fast feedback loops so that Devs have tools to be confident in the code. They remove human error and automate analysis of deployed versions to give Devs insight. 

For devs, they should know whether the solutions create unexpected problems via a pipeline and then resolve the issues within minutes.

Everyone in DevOps know that changes made and released haven’t broken the product. Therefore, the project is always in a deployable and shippable state. This includes automating testing, the build and deployment, and how people interact with it.

CI/CD steps allow us to do this automatically. The same goals are achieved with high level testing end-to-end versus human testers. 

### Advanced testing


#### Parameterized tests

Allows us to automate the running of a test across a range of values, done with `@ParameterizedTest` wither from an explicit list `@ValueSource` or `@CsvSource`. This allows us to more easily specifiy edge cases, boundary tests, etc.

![](Pasted%20image%2020251027141437.png)

#### Repeated tests

Good for non-deterministic tests, e.g. remote access, network issues. ‘If it fails twice or more out of 8 times then there is some issues”/

> coursework: probably not useful


![](Pasted%20image%2020251027141455.png)


#### Performance testing

Useful for algorithms

![](Pasted%20image%2020251027141518.png)


#### Test tagging

> Coursework: is usefulk

Tags can be any plaintext to want, so that a pipeline or configuration only runs certain tests at a different times. For example it can only run tests for a given area of the project, or the area currently working on.

e.g.:
- Basic tests that are always run
- Integration tests when merging into dev
- Release tests when creating a release

```java
@Test
@Tag(“Taxes”)
void testingTaxBrackets() {
	// do something
}

```

This allows Maven/Gradle to do specific tests depending on setup, e.g. on release. 


### Test smells

- Assertion roulette - uncommented, undocumented asserts
- Default tests/Empty tests - initial/template/old test functions
- Duplicate asserts - twice with the same variable, should be something else
- Handling exceptions badly - features of JUnit should assert that an error should throw, not having a fail command if catching an error

### Regression tests


The aim of regression tests is to prove that a system as a whole works as intended while being changed. Unit tests cannot do this as units are what are being changed. Regression tests check when something is ready to go to the next change - and work on higher-level classes, that show that the outcome passes even with changes made below. 

It allows us to prove that e.g. class B is not relying on class A unintentionally - avoiding unexpected issues or changes in function/performance. 

This allows bugs to be fixed, Devs given evidence of success, QA team assurance there is no unexpected issues. They can be highly automated.

Types of regression tests include, typically automated in the CI/CD pipeline:
- Unit regression testing: tests should act as simple regression tests for a unit
- Progressive RT - when working on tests that will use the outcome of the area being changed. This shows that by the end the new feature works as intended. “Tag them with a new feature, and run the tags for this featuer”
- Selective RT - “this class will affect 4 other classes, so check that these and only these work after the change”
- Partial RT - run all tests for the reported feature to make sure it still works
- Complete RT - run every test for the whole software to make sure nothing randomly broke somewhere else

The reason there are many of these tests with different scopes is primarily due to speed. It can take a long time for millions of lines of code from thousands of developers for e.g. a Chrome release. It can slow down a server and prevent other tests running for other developer pushes for a long time.


### Analysing regression tests

Some RTs can directly fail, but some not. Some might not fail on assert but create lots of system data, analyse this and run a fail command, or create a graph that someone clearly sees an error with. 


While it is important to do this, it is not always easy to achieve. Comprehensively testing everything is painful (so many features, extra infra costs) so it needs to be balanced with “what we need to know” versus “what is nice to have”. 

Tests are designed to work on a specific area - however it is hard to partial RTs without running the whole system. “Mocking” classes and services on the system (e.g. “always assume the database outputs this whenever I say this”) is commonly used. Mockito is used for Java with mock classes with `@Mock`.

![](Pasted%20image%2020251027143457.png)

In documentation: “All of my tests will assume that X will return Y”

A stub is an empty method created in code, ready to build after the test, that returns something valid for compilation. Then, the test for the correct behaviour is written. Then the stub is converted into a real method.
Mockito stubbing is creating temporary behaviours just enough for the test to pass.


### End-to-end (E2E) testing

”If the user clicks these buttons, then it should show Y.” It implies that all frontend, backend, database and API should all work together and in an expected way. It tests the complete User eXperience is working (and all components are all functioning) - simulating true user interaction.

E2E is the closes to acceptance testing. It is even more time consuming and resource-heavy than RTing, based on original user requirements, and is only really run on release versions before alpha testing. 

>There are frameworks that click every button to make sure nothing breaks, and if something does, it displays the list of all things pressed/interacted that led to the failure.

### E2E with JavaFX / TestFX

![](Pasted%20image%2020251027144343.png)

Allows a test to press each button and verify that it has become clickable 
and states of each interface object is as expected.

## Maven and Gradle

These are auto-build systems that define which packages are to be built, how to build them, with goals “in test mode, do X; in release, do Y”, making it useful for CI/CD. “run all the tests with these packages and if it pases, build the jar file in Z”.

This module uses Maven

`pom.xml` 

![](Pasted%20image%2020251027144953.png)

If goal is to check vs release: use different plugins for checking and releasing.


Means if there is a goal of high level to run high-level tests, then run them but 















