# CS2103: Unified Modeling Language (UML)

## Class diagrams
A **class diagram** describes the structure of a system by showing the system's classes, their attributes, methods, and relationships among objects.

<img src="https://cdn.rawgit.com/irvinlim/cs2103-notes/master/images/class-diagram.svg">

### Relationships
<img src="https://cdn.rawgit.com/irvinlim/cs2103-notes/master/images/uml-arrows.svg" width="400">

- **Association**: `A` is associated with `B` if `A` holds a reference to `B` at the class level.
  - e.g. A `Table` instance holds an array of `Chair` instances, declared at the class level.
- **Dependency**: `A` depends on `B` (or `A` has a dependency on `B`) if `A` receives a reference to `B` via method parameters, or if `A` uses a method or field in `B`.
  - e.g. A `Player` depends on `SixSidedDie`, as it has a method with signature `void takeTurn(SixSidedDie die)`, which also calls `die.roll()`.
- **Composition**: Represents "whole-part" relationship, and implies instance creational responsibility. This means that if `A` composes `B` (or `B` is composed in `A`), then if `A` is destroyed, so will all of `B` inside of it.
  - Also implies that there **cannot be cyclical links**. A composition relation from `A` to `A` implies that `A` can compose another instance of `A`, but never itself. (without composition, it implies that it can.)
- **Aggregation**: Represents "container-contained" relationship. Not recommended to be used.

#### Inheritance
- **Generalization**: Also known as *extending* in Java terms. `A` is a generalization of `B` if `A` extends `B` (`B` is the superclass of `A`).
- **Realization**: Also known as *implementing* in Java terms. `A` is a realization of `B` if `A` implements `B` (`B` is an interface).

#### Navigability
Navigability indicates whether a class involved in an association is "aware" of the other participating class. `A` is navigable to `B`, *if and only if* `A` contains a reference to `B`.

Navigability is shown by having an arrowhead pointing in the direction of navigability. An association can be either navigable unidirectionally or bidirectionally. Note that if no arrowheads are shown, it is implied to be either unspecified or bidirectional navigability.

#### Associations as attributes
Associations (denoted by lines between two classes) can be replaced by an attribute in the enclosing class, hence removing the connecting line.

#### Association classes
Sometimes there needs to be a class to store additional information about an association - for example, the `marriageDate` of a `Marriage` association between a `Husband` and a `Wife`.

<img src="https://cdn.rawgit.com/irvinlim/cs2103-notes/master/images/association-class.svg" width="300">

### Visibility
- `+`: `public`
- `-`: `private`
- `#`: `protected`
- `~`: `package`

### Multiplicity
Multiplicity is the number of objects of a class that participate in the association. The multiplicity of `A` in relation to `B` refers to how many objects of `A` are associated with one object of `B`.

Commonly used multiplicities:
- `0..1`: optional, can be linked to 0 or 1 objects. Also called **optional association**.
- `1`: compulsory, must be linked to one object at all times. Also called **compulsory association**.
- `*`: can be linked to 0 or more objects.
- `n..m`: the number of linked objects must be `n` to `m` inclusive

## Object diagrams
An **object diagram** shows an object structure at a given point of time while a class diagram represents the general situation.

<img src="https://cdn.rawgit.com/irvinlim/cs2103-notes/master/images/object-diagram.svg" width="500">

## Sequence diagrams
A **sequence diagram** captures the interactions between multiple objects for a given scenario.

<img src="https://cdn.rawgit.com/irvinlim/cs2103-notes/master/images/sequence-diagram.svg" width="1000">

### Elements of SD
- **Entities**: Actors or components involved in the interaction
- **Instance**: An instantiated object of a class
  - The instance name follows the format `InstanceName:ClassName` for a named instance, or just `:ClassName` to represent an unnamed instance
- **Lifeline**: This shows the time period in which the instance is alive
- **Activation Bar**: This is the period during which the instance is in control of the execution
- **Operation**: A method name or description of a user interaction that acts as an input to the following instance
- **Return value**: The return value of a method, or the output that is returned from the prior instance

To reduce clutter, activation bars and return arrows may be omitted if they do not result in ambiguities or loss in information

### Operation details
- **Operation**: `methodName(): ReturnType`
- **Description**: Description of what the method does.
- **Preconditions**: The conditions that must be true before calling this operation.
- **Postconditions**: Describe the system after the operation is complete.

### Object creation and destruction
Operations which instantiate a new instance of an object can be represented using **object creation**. The activation bar for the constructor follows right after the instance box (see below).

Destruction causes the lifeline to stop at the point of destruction. It has no return value. In languages with automatic memory management (e.g. Java), destruction is usually not depicted or handled by the developer.

<img src="https://cdn.rawgit.com/irvinlim/cs2103-notes/master/images/creation-destruction.svg" width="400">

### Self-calls
Objects can call operations which invoke its own methods (sending messages to itself) using **nested activation bars**.

### Frames
Operations or sequence diagrams can be wrapped in multiple types of frames.

- `loop`: Executes actions in the frame repeatedly until the *predicate* returns false.
- `ref`/`sd`: Create a **reference** to another sequence diagram by name. The referenced SD is wrapped in a `sd` frame.
- `opt`: Represents an **optional** frame. Actions are executed if the predicate is true.
- `alt`: Represents an if-else construct. Actions will be executed in either the first or second fragment (mutually exclusively) depending if the *predicate* is true.
- `par`: Represents two or more executions that will run in parallel. Each fragment represents the actions running on a single thread.

## Activity diagrams
An **activity diagram** can be used to describe a workflow, and consists of a sequence of actions and control flows. 

- **Action**: A single step in an activity. 
- **Control flow**: Shows the flow of control from one action to the next.
- **Branch/merge nodes**: Represents alternative (if-else) paths, depending on whether the *guard condition* is satisfied.
- **Forks/joins**: Represents parallel/concurrent flows of control. All concurrent paths should complete at the *join* before execution is allowed to continue after on the outgoing control flow.
- **Rake**: Represents the inclusion of an external control flow, found in a subsidiary diagram.

<img src="https://cdn.rawgit.com/irvinlim/cs2103-notes/master/images/activity-diagram.svg" width="800">

### Swimlane diagrams
A **swimlane diagram** is an activity diagram which is partitioned to identify the actors involved in each action.

## Conceptual class diagram/OO domain model
A class diagrams which is used to model the problem domain is a **conceptual class diagram**. Classes in domain models do not have a compartment for methods. It is also common to omit navigability from domain models.