# CS2103: Testing

## Definition
> Operating a system or component under specified conditions, observing or recording the results, and making an evaluation of some aspect of the system or component
> (definition by Institute of Electrical and Electronics Engineers (IEEE))

Testing entails the execution of a set of test cases to test the **software under test (SUT)**. A test case may contain:
- Execution
  - Input
  - Expected behaviour
  - Cleanup code (if any)
- Documentation
  - Unique identifier
  - Descriptive name
  - Objectives
  - Classification

A test case failure is a mismatch between the expected and actual behaviour.

### Scripted vs exploratory testing
- **Exploratory testing**: Simultaneous learning, test design, and test execution whereby the nature of the follow-up test case is decided based on the behavior of the previous test cases.
  - Also known as reactive testing, error guessing technique, attack-based testing, and bug hunting
  - Depends on the tester's prior experience and intuition. Should be done by experienced testers using a clear framework.
- **Scripted/proactive testing**: Use a predefined set of test cases.
  - More systematic, and hence likely to discover more bugs
  - Takes more time since test case scripts have to be written

### Black-box vs white-box
This categorization depends on how much internal details are considered when designing test cases. 

- In the **black-box approach**, also known as *specification-based* or *responsibility-based testing*, test cases are designed exclusively based on the SUT’s specified external behavior.
- In the **white-box** approach, also known as *glass-box* or *structured* or *implementation-based testing*, test cases are designed based on what is known about the SUT’s implementation, i.e. the code.
- **Gray-box testing** refers to a mixture of both - knowing some knowledge about the code will help to generate more useful test cases, while still testing on a higher-level basis.

### Regression testing
A **regression** occurs when a system is modified after it has been tested, and the modification resulted in unintended and undesirable effects on the system.

Regression testing is to detect and correct regressions. It is more effective when done frequently, so it is more practical to automate regression tests.

### Testability
**Testability** is an indication of how easy it is to test an SUT. As testability depends a lot on the design and implementation. We should try to increase the testability of our software when we design and implement them.

## System testing
**System testing** is testing of the software application as a whole to check if the system is complaint with the user requirements. It is an end to end user perspective testing intended to find defects in the software system.

System testing is a type of black box testing technique thus the knowledge of internal code in not required. It is a high level testing always performed after integration testing. Regression and Retesting is performed many times in system testing. The user can perform different type of tests under System testing. It would depend on the user or the organisation to choose which type of system testing should be performed on the application. 

System testing can be broadly classified in two types:

- Functional testing
- Non-functional testing

System testing is performed to check the following points:

- To check whether the software system is made according to the customer needs written in Software Requirements Specifications, it meets both functional and non-functional design requirements of the system.
- When all the modules are combined as a whole, many errors and facts may arise which may not give the expected results? So system testing is performed to find the defects or bugs in all the interfaces as well the whole system.
- To execute the real–life scenarios on the software. It is done on the staging server which is very much similar to the production server where the software would actually be deployed. The system test cases are made according to the end-to–end use perspective.

## Unit testing
**Unit testing** involves testing individual units (methods, classes, subsystems, etc.) and finding out whether each piece works correctly in isolation. A proper unit test require the unit we are testing to be isolated from other code.

Unit testing may require test drivers. A test driver is a module written specifically for testing. A test driver’s job is to invoke the SUT (Software Under Test) with test inputs. Test drivers are required for unit testing as most of the units do not have a UI. 

### Using stubs/mocks
A **stub/mock** is a dummy component that receives outgoing messages from the SUT, and are used in place of collaborating objects in order to isolate the SUT from other objects. Doing this prevents bugs within the collaborating objects from interfering with the test. A stub has essentially the same interface as the collaborator it replaces, but its implementation is meant to be so simple that it cannot have any bugs.

A stub usually does the following:

- Nothing at all
- Log data to a file
- Return hard-coded responses

### Dependency injection (DI)
**Dependency injection** is the process of "injecting" objects to replace current dependencies with a different object. It allows a program to follow the [Dependency Inversion Principle (DIP)](principles.md#dependency-inversion-principle-dip).

Dependency injection means that dependencies should not be hard-coded in, but instead all potential dependencies should be dependent on a common interface, and passed in via setters or constructors.

#### Dependency injection for five-year-olds
> When you go and get things out of the refrigerator for yourself, you can cause problems. You might leave the door open, you might get something Mommy or Daddy doesn't want you to have. You might even be looking for something we don't even have or which has expired.
>
> What you should be doing is stating a need, "I need something to drink with lunch," and then we will make sure you have something when you sit down to eat.

## Integration testing
**Integration testing** tests the interface between modules of the software application. Integration tests aim to discover bugs in the "glue code" that are often the result of misunderstanding of what the parts are supposed to do vs what the parts are actually doing. The different modules are first tested individually and then combined to make a system. It is conducted after unit tests, because the parts must work before the whole does.

There are different techniques available for integration testing:
- **Big Bang Integration Testing**: In type of integration testing all the modules are combined first and then tested together.
- **Top-to-Bottom Integration Testing**: This type of testing take place from top to bottom uses Stubs which are substitutes of components. The top module is tested first.
- **Bottom-to-Top Integration Testing**: This type of testing take from bottom to top and uses Drivers which are substitutes of components. The bottom module is tested first.

Integration testing is performed to check the following points:

- To check whether the modules developed by individual developers when combined are according to standards and gives the expected results.
- When modules are combined, sometimes the data travelling between modules has many errors which may not give the expected results. So integration testing is performed to find the defects or bugs in all the interfaces.
- To check the integration between any third party tools used

## System testing
**System testing** tests the whole system against the system specification, usually done by a testing team/QA team. System test cases are based exclusively on the specified external behavior of the system. It also aims to tests [non-functional requirements](requirements.md#non-functional-requirements-nfrs), such as:

- **Performance testing**: Ensure the system responds quickly.
- **Load testing/stress testing/scalability testing**: Ensure the system can work under heavy load.
- **Security testing**: Test how secure the system is.
- **Compatibility testing/interoperability testing**: Check whether the system can work with other systems.
- **Usability testing**: Test how easy it is to use the system.
- **Portability testing**: Test whether the system works on different platforms.

## Acceptance testing
**Acceptance testing** or **user acceptance testing (UAT)** is carried out to show that the delivered system meets the requirements of the customer. Similar to system testing, it tests the system as a whole, but against the *requirements specification*. It comes after system testing, and is usually done by a team that represents the customer (project managers).

Note that the *requirements specification* could be limited to how the system behaves in normal working conditions, while the *system specification* can also include details on how it will fail gracefully when pushed beyond limits, how to recover, additional APIs not available for users (for the use of developers/testers), etc.

Acceptance tests gives an assurance to the customer that the system does what it is intended to do. Besides, acceptance testing is important because a system could work perfectly on the development environment, but fail in the deployment environment due to subtle differences between the two.

## Alpha and Beta testing
**Alpha testing** is performed by the users, under controlled conditions set by the software development team. **Beta testing** is performed by a selected subset of target users of the system in their natural work setting. An **open beta** release is the release of not-yet-production-quality-but-almost-there software to the general population.

## Designing test cases
Test cases should be **effective** and **efficient**. 

### Equivalence partitioning (EP)
**Equivalence partitioning** is a technique that uses the observation that *any input in a partitioned range of values are likely to behave in the same way*, in order to improve the efficiency and effectiveness of testing. By dividing possible inputs into groups which are likely to be processed similarly by the SUT, testing every possible input in each group is avoided. Testing one of the inputs for a given range should be as good as exhaustively testing all inputs in that range.

### Boundary Value Analysis (BVA)
**Boundary value analysis** is based on the observation that bugs often result from incorrect handling of boundaries of equivalence partitions. When doing boundary value analysis, values around the boundary of an equivalence partition are tested. Typically, three values are chosen: one value from the boundary, one value just below the boundary, and one value just above the boundary.

### Testing combinations
Instead of exhaustively testing all possible combinations, we can instead just choose to include a value at least once in the test cases. However, when testing for negative test cases, **invalid values should not be combined**, as it does not guarantee that the correct error is being caught; instead test invalid values in separate test cases.

### Testing use cases
**Use case testing** is straightforward in principle: test cases are simply based on the use cases. It is used for system testing (i.e. testing the system as a whole).

## Test-Driven Development (TDD)
Typically, tests are written after writing the SUT. However, TDD advocates writing the tests before writing the SUT. In other words, first define the precise behavior of the SUT using test cases, and then write the SUT to match the specified behavior. While TDD has its fair share of detractors, there are many who consider it a good way to reduce defects. 

Note that TDD does not imply writing all the test cases first before writing functional code. Rather, proceed in small steps:

1. Decide what behavior to implement.
2. Write test cases to test that behavior.
3. Run those test cases and watch them fail.
4. Implement the behavior.
5. Run the test case.
6. Keep modifying the code and rerunning test cases until they all pass.
7. Refactor code to improve quality.
8. Repeat the cycle for each small unit of behavior that needs to be implemented.

## Test coverage
**Test coverage** is a metric used to measure the extent to which testing exercises the code. Several indicators could be used:

- **Function/method coverage**: In terms of number of methods executed in the test
- **Statement coverage**: In terms of lines of code executed in the test
- **Branch coverage**: Whether both branches (i.e. both if and else) are executed in tests
- **Condition coverage**: Stricter than branch coverage, and aims to measure whether each case in combined conditionals (using `&&` or `||`) are fully tested.
- **Path coverage**: Using *Control Flow Graphs (CFGs)*, which represents all possible paths of a software in a graph (i.e. graph with vertices and edges), measure how many paths are covered.
- **Entry/exit coverage**

## Other QA techniques
There are other QA techniques that do not involve executing the SUT.

- **Inspections & reviews**: Inspections involve a group of people systematically examining a project artefact to discover defects. 
  - An advantage of inspections is that it can detect functionality defects as well as other problems such as coding standard violations.
  - A disadvantage is that an inspection is a manual process and therefore, error prone.
- **Formal verification**: Formal methods is using mathematical and computer science concepts to prove the correctness of a program.
- **Static analyzers**: These tools automatically analyze the code to find anomalies such as unused variables and unhandled exceptions.