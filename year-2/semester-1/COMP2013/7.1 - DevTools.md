
JavaFX and TestFX


> Think about design of tests in task 3 which will then have to be refactored in TestFX


Using JUnit5 with TestFX.

To use it, we use:
```
@ExtendWith(ApplicationExtension.class)
```
We extend the JavaFX class with this.

Then, we use BeforeAll-type code, we use @Start to start up some code before each test. It loads the interface each time and then runs the test each test. 

Then, we can use @AfterEach to reset data e.g. a database or data that will then be stored.

- Label tests with `@TestFX`
- Each test should have `(FxRobot robot)` as a parameter

Each robot can then interact with: 
- robot.clickOn()
- .doubleClickOn()
- .rightClickOn()
- .moveTo() and .dragTo() and .scroll(
- .closeCurrentWindow()
- .type() and .write() and .eraseText ()
- .press(), .push(), .release() - keys

`import org.testfx.api.FxAssert;`

Can refer to any object in the view with a hash then its name (like HTML) - if any object has text
```java
FxAssert.verifyThat("#myButton", LabeledMatchers.hasText("click me!"));
```

We can also use normal asserts with: 
```java
import org.testfx.assertions.api.Assertions;

import org.testfx.framework.junit5.ApplicationExtension;

import org.testfx.framework.junit5.Start;

Assertions.assertThat(robot.lookup("#myButton").queryAs(Button.class)).hasText("click me!");
```


### Live demo notes

In Maven:
- add a `<dependency>` being `org.TestFX` with the appropriate version
- add a `<plugin>`, being `<groupid>org.apache.maven.plugins`
- then compile, new directory, click tests directory recommendation

The test class should use:
`@ExtendsWith`

each file within should be labelled with `@Test`

`FXAssert.verifyThat(“WelcomeText”.labeMatcher.hasText(“welcome”))`

> Coursework: use the system that builds the test coverage (Maven) to test and achieve 80% coverage.

!!TODO: Do rewatch lecture notes
### Javadoc

Is a great tool for code commenting, and creates a retro 90s looking web interface.

It forces developers to use a specific way with clear examples, with less typing and more automation.

It generates an easy HTML-based output as a living documents. We can use `@<tag>` to pass in tags to the HTMl. 
https://www.oracle.com/uk/technical-resources/articles/java/javadoc-tool.html#examples

At the class-level, we can use @author to specify the author of the class, and then appending multiple authors afterwards. We can use @version to specify the version of it, used with the %i% macro. 

For ech method, we can use @param (one per line) and @return for any non-void value. @throws (in alphabetical order) if it throws an exception. 

@since specifies when the class/method was added to hte project, and @deprecated explains why and when it was, alongside alternatives.

@see means “see also” - useful to show devs other text, html, or specific files and functions. @link creates htm cross-reference links.

The javadoc will always take the first sentence for a summary table (the always full stop followed by a whitespace). Descriptions should come before the first list of @tags, with paragraphs separated with `<p>`. The @tag means the description is now over.

Javadoc automatically handles inheritance and combines information to cross-reference other classes. Override methods are listed in the original description of the superclass in the overrides section. 

### IntelliJ features

Debug information can include breakpoints and conditional breakpoints that must match a certain condition for them to be triggered.

Settings -> Plugins -> CheckStyle and find CheckStyle IDEA. Then Tools -> CheckStyle and say Google’s standard. Then can run inspection in File -> Analyse -> Inspect to see checkstyle use
















