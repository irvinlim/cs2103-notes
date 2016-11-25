# CS2103 Lecture 2.1: Code Quality

## Coding standard
A coding standard should be followed. An example of such a coding standard can be found [here](https://oss-generic.github.io/process/codingstandards/coding-standards-java.html).

## Naming conventions
- Related things should be named similarly, while unrelated things should not.
- Use **nouns for classes/variables**, and **verbs for methods**.
- Don't use case or numbers to distinguish variable names.
- Distinguish clearly between single- and multi-valued variables.
  - e.g. `Person student` vs `List<Person> students`

## Making syntax obvious
- Use explicit type conversion (typecasting) instead of implicit.
- Use parentheses/braces even when unecessary:

```java
// Don't do this:
if (isTrue)
  doSomething();

// This is preferred.
if (isTrue) {
  doSomething();
}
```

- Use enumeration instead of arbitrary integers.
  - e.g. Instead of having a variable `state` take integer values 0, 1, 2, use `enum` to declare state as follows:

```java
public enum State {
  STARTING, ENABLED, DISABLED
}
```

- Methods that need to be called in a particular order should be made obvious.
  - e.g. Methods should be called `phaseOne()` and `phaseTwo()` if necessary.

## Don't misuse syntax
- The `default` option in a case statement or `else` in an if-else construct should be used for the intended default action/catch errors, and not to execute the last option. 

```java
// Instead of this:
if (red) {
  print("red");
} else {
  print("blue");
}

// Do this:
if (red) {
  print("red");
} else if (blue) {
  print("blue");
} else {
  throw new InvalidInputException("Invalid colour provided.");
}
```

- Variables should be single-use. Don't reuse variables for a different purpose.
- Don't redeclare method parameters inside a method body.
- Avoid data flow anomalies, such as using variables before initialization.

## Avoid error-prone practices
- Never write a case statement without the 'default' branch.
- Never write an empty 'catch' statement.
- All 'opened' resources must be closed explicitly. If it was opened inside a 'try' block, it should be closed inside the 'finally' block.
- If several methods have similar parameters, use the same parameter ordering.
- Do not include unused parameters in the method signature.
- Whenever an arithmetic calculation is performed, check for overflow and 'divide by zero' errors.

## Minimize global variables
Global variables may be the most convenient way to pass information around, but they do create implicit links between code segments that use the global variable. Avoid them as much as possible.

## Avoid magic numbers/strings
- Avoid indiscriminate use of numbers as constants all over the code. Define them as named constants, preferably in a central location. 
  - e.g. `3.1415` as the mathematical constant PI
- Avoid using string literals with special meanings.
  - e.g. `"Error 1432"`
- Make calculation logic explicit rather than using the final value.
  - e.g. Instead of `return 9`, do `return MAX_SIZE - 1`.

## Minimize duplication
- **Don't Repeat Yourself (DRY) principle**: Code duplication, especially when you copy-paste-modify code, often indicates a poor quality implementation.
  - Functionality required in more than one place should be extracted into a relevant location that all relevant parts can access.

## Comment minimally, but sufficiently
- Avoid writing comments to explain bad code. Improve the code to make it self-explanatory.
- Do not use comments to repeat the obvious.
- Do not write comments as if they are private notes to self. Instead, write them well enough to be understood by another programmer.
- Explain 'why' and 'what' aspect of the code, rather than the 'how' aspect. (i.e. the high-level idea of the code)

## Be simple
- **Keep it simple, stupid (KISS) principle**: Sometimes the simplest solutions are the best ones.
- Do not readily dismiss the brute-force yet simple solution for a complicated one, unless your application justifies the need for high-performance requirements.

## Code for humans
- Always assume that "anyone who reads the code you write is dumber than you".
- Avoid long methods. (e.g. don't exceed 50 LoC that go past the computer screen)
- Limit the depth of nesting. (e.g. don't use more than 3 levels of nesting)
  - Avoid arrowhead-style code. Use short-circuit evaluation if you are able to.
- Limit to one statement per line.
- Avoid complicated expressions - split the calculation or evaluation up into different logical steps.
- The default path of execution should be clear. Exceptions or "unusual" cases should be in **guard clauses**:

```java
// Don't do this:
if (!isUnusualCase) {
    if (!isErrorCase) {
       start();
    } else {
        handleError();
    }
} else {
     handleUnusualCase();
}

// Instead, do this:
if (isUnusualCase) {       // Guard clause #1
    handleUnusualCase();
    return;
}

if (isErrorCase) {         // Guard clause #1
    handleError();
    return;
}

start();
```

## Single Level of Abstraction Principle (SLAP)
- Each method should be written in terms of a single level of abstraction.
- If there is a statement which belongs to a lower level of abstraction, it should go to a private method which comprises statements on this level.
- Often the body of a loop can be extracted resulting in a separate private method.
