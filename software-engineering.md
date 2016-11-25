# CS2103: Sofware Engineering Concepts

## Integrated Development Environments (IDEs)
An IDE generally consists of:
- A source code editor that includes features such as syntax coloring, auto-completion, easy code navigation, error highlighting, and code-snippet generation.
- A compiler and/or an interpreter (together with other build automation support) that facilitates the compilation/linking/running/deployment of a program.
- A debugger that allows program errors to be located.

## Debugging
- By inserting temporary print statements
  - Simplest method to do ad-hoc debugging, but increases the risk of introducing bugs into the program
- Manually tracing the code (eye-balling)
  - Difficult and time-consuming
- Using a debugger
  - Allows pausing of execution, and stepping through/into/out of statements one at a time, while examining the internal state if necessary.

## Assertions
**Assertions** are used to confirm assumptions about the program state. It is recommended that assertions be used liberally in the code.

## Logging
**Logging** can be useful for troubleshooting problems that exceptions and assertions could not prevent (due to the failure to cater for certain situations). A good logging system records some system information regularly. When bad things happen to a system, their associated log files may provide indications of what went wrong and action can then be taken to prevent it from happening again.

## Defensive programming
**Defensive programming** is a form of defensive design intended to ensure the continuing function of a piece of software under unforeseen circumstances. A defensive programmer proactively tries to eliminate any room for things to go wrong. Data validation is an example of defensive programming practice.

Defensive programming usually tries to handle exceptions and errors gracefully.

- **Enforcing 1-to-1 associations**: For classes with unidirectional one-one associations (e.g. composition), create the child instance once the parent is instantiated.
  - e.g. When instantiating a `new Door()`, the `Door` constructor should instantiate `new DoorHandle()`, so that `_doorHandle` will never be null.
- **Enforcing referential integrity**: For classes with bidirectional one-one assocations, enforce checks and update links when references are updated.
  - e.g. When using the `setSpouse(Person spouse)` method, also invoke `spouse.setSpouse(this)` if the spouse is different.
- **Design-by-Contract**: It is the responsibility of the caller to ensure all preconditions are met. The method should check if any precondition is not fulfilled, before executing the body of the function.

### Overly defensive programming
Programming style that is considered **overly defensive** when code is written to catch or prevent too many exceptions, to the point that errors go suppressed and unnoticed.

### Offensive programming
**Offensive programming** is considered the other extreme of defensive programming, where errors should be thrown rather than degraded gracefully. It prioritizes the detection of bugs rather than the hypothetical safety benefit of tolerating them.

## Software architecture
The **software architecture** shows the overall organization of the system. System architecture addresses the big picture and usually consists of a set of interacting components that fit together to achieve the required functionality.

### Architectural styles
- **Multitier/n-tier style**: Higher layers make use of services provided by the lower layers.
  - e.g. Presentation-Logic-Data three-tier architecture.
- **Client-server style**: A central server provides services to multiple other clients.
- **Transaction processing style**: A *dispatcher* receives *transactions* from each client, and then dispatches it to the relevant service.
- **Service-oriented architecture (SOA)**: Having several microservices, where each server hosting each microservice is in charge of a single task. Communication between services and clients are done over the network.
- **Event-driven architecture**: Events are occurences which occur outside of the software, such as button presses. Such events are detected and handled by the software, which act only upon the event.

### Application Programming Interface (API)
The API of a component or software is the list of public operations supported by a component and what each operation does. An API is a contract between the component and its users. It should be well-designed (i.e. should cater for the needs of its users) and well-documented.

### Design approaches
- **Top down vs bottom up**: 
  - When using *top down design*, low level details are not considered until much later in the design process, and is often used when creating a big product from scratch. 
  - Comparatively, *bottom up design* is starting with lower level details (e.g. data structures, storage formats, functions etc.) and progressively grouping them together to create bigger components, and is often adopted when the system is small or when developing a variant of a previous product whereby a large collection of reusable assets can be used in the new product.
- **Agile vs full-design-up-front/waterfall**:
  - *Agile methodology* prefers sprints and iterations which delivers usable products at the end of each cycle. It is considered enough if the design can support the feature that is going to be implemented in the immediate future.
    - e.g. Scrum, Kanban
  - The *waterfall model* is the traditional method of designing software, where the design ensures that it supports all possibilities and all potential features.
    - The model goes by: Requirements, Design, Implementation, Verification, Maintenance - sequentially in that order.

## Integration
The integration of software components written by different team members can be done in two distinct ways.

- **Late, one-time**: In this extreme case, developers wait till all components are completed and integrate all finished components just before the release.
  - Not recommended because: Late integration → incompatibilities found → major rework required → cannot meet the delivery date.
- **Early and frequent**: Instead of waiting till the end, each part of the software should be integrated early and frequently, and allow the product to evolve in parallel in small steps. This can be done by one developer, possibly the one in charge of integration. 

### Order of integration
- **Big-bang integration**: All components are integrated at the same time. This is not recommended as it is more unsystematic, uncovering too many bugs at the same time.
- **Incremental integration**: 
  - **Top-down integration**: Higher-level components are integrated before bringing in the lower-level components. 
    - *Advantage*: Higher-level problems can be discovered early.
    - *Disadvantage*: Requires the use of stubs in place of lower-level components until the real lower-level components are integrated.
  - **Bottom-up integration**: The opposite of *top-down integration*, which favours details over the big picture.
  - **Sandwich integration**: A mix of both.

## Build automation
**Build automation** is performed on relatively larger software, where the building of the software consists of multiple steps, such as pulling from the RCS, compilation, updating links and documents, packaging, pushing back to RCS, deploying on a remote server, emailing, cleanup, and so on. Examples of build tools are GNU's `make`, Apache Ant, Maven and Gradle.

## Dependency management
**Dependency management** tools automate the management of third-party libraries and dependencies, downloading and updating regularly.

## Continuous Integration (CI)
**Continuous integration** is the practice of building and testing happening at each development step, such as at every `git push`. It is intended to prevent "integration hell".