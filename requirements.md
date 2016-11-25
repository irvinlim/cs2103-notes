# CS2103 Lecture 5.2: Software Requirements

## Requirements
A **requirement** specifies the intended usage of a software product. A development project may aim to replace or update an established software system (called a brown-field project) or it may aim to develop a totally new system with no precedent (called a green-field project).

### Functional requirements
Functional requirements specify what the system should do.

### Non-functional requirements (NFRs)
Non-functional requirements specify the constraints under which system is developed and operated.

Some examples of non-functional requirements:
- Data requirements e.g. size, volatility, persistency etc.,
- Environment requirements e.g. technical environment in which system would operate or need to be compatible with.
- Accessibility, capacity, compliance with regulations, documentation, disaster recovery, efficiency, extensibility, fault tolerance, interoperability, maintainability, privacy, portability, quality, reliability, response time, robustness, scalability, security, stability, testability, and more...

## Establishing requirements
There are many techniques used during a requirements gathering. The following are some of the techniques.

### Brainstorming
Brainstorming is a group activity designed to generate a large number of diverse and creative ideas for the solution of a problem. In a brainstorming session there are no "bad" ideas. The aim is to generate ideas; not to validate them. Brainstorming encourages you to "think outside the box" and put "crazy" ideas on the table without fear of rejection.

### User surveys
Carefully designed questionnaires can be used to solicit responses and opinions from a large number of users regarding any current system or a new innovation.

### Observation
Observation of users in their natural work environment is a common technique used to understand the tasks and the environment of the user. Interaction logging on an existing system can also be used to gather information about how an existing system is being used.

### Interviews
Interviewing potential stakeholders and domain experts can give us useful information about a domain. Interview is a good technique at getting users to explore what users feel about the required system. Interviews also provide opportunities for the development team members to meet stakeholders and to make stakeholders feel involved in the development process.

### Focus groups
Focus groups are a kind of informal interview within an interactive group setting. A group of people (e.g. potential users, beta testers) are asked about their understanding of a specific issue or a process. Focus groups can bring out undiscovered conflicts and misunderstandings among stakeholder interests which can then be resolved or clarified as necessary.

### Prototyping
A prototype is a mock up, a scaled down version, or a partial system constructed
- to get users’ feedback.
- to validate a technical concept (a "proof-of-concept" prototype).
- to give a preview of what is to come, or to compare multiple alternatives on a small scale before committing fully to one alternative.
- for early field-testing under controlled conditions.

Early UI prototyping, i.e. sketching the user interface for the intended product, is a good technique to uncover requirements, in particular, those related to how users interact with the system. UI prototypes are often used in brainstorming sessions, or in meetings with the users to get quick feedback from them.

## Analyzing similar products and documentation
Studying existing products can unearth shortcomings of existing solutions that can be addressed by a new product. For example, when developing a game for a mobile device, a look at a similar PC game can give insight into the kind of features and interactions the mobile game might offer. Product manuals and other forms of technical documentation of an existing system can be a good way to learn about how the existing solutions work.

## Specifying Requirements

### Textual descriptions (unstructured prose)
A textual description can be used to give a quick overview of the domain/system that is understandable to both the users and the development team. Textual descriptions are especially useful when describing the vision of a product. This is the most straight forward way of describing requirements. However, lengthy textual descriptions are hard to follow.

### Feature list
A list of features (or functionalities) grouped according to some criteria such as priority (e.g. must-have, nice-to-have, etc. ), order of delivery, object or process related (e.g. order-related, invoice-related, etc.).

### User stories
User stories are brief (typically, 1-3 sentences) descriptions of what the system can do for the users, written in the customers’ language. Often, user stories are written by the customers themselves. User stories are mainly used for early estimation and scheduling purposes.

A commonly used format for writing user stories is:
> As a `<use type/role>` I can `<function>` so that `<benefit>`.

The biggest difference between user stories and traditional requirements specifications is in the level of detail. User stories should only provide enough detail to make a reasonably low risk estimate of how long the story will take to implement. When the time comes to implement the story, the developers will meet with the customer face-to-face to work out a more detailed description of the requirements.

User stories are often written on index cards or sticky notes, and arranged on walls or tables to facilitate planning and discussion.

#### Levels of user stories
High-level user stories, sometimes called **epics** or **themes**, can cover a big functionality. They can be further split into multiple lower-level user stories.

#### Conditions of satisfaction
We can add **conditions of satisfaction** to a user story to specify things that need to be true for the user story implementation to be accepted as 'done'. 

### Use cases
> A description of a set of sequences of actions, including variants, that a system performs to yield an observable result of value to an actor.

A **use case** describes an interaction between the user and the system for a specific functionality of the system (i.e. 'cases of users using the system'). A use case model is a way of capturing the functional requirements of a system. Use cases are a part of the UML modeling notation.

#### Components of a use case
- **Actor**: The *role* played by the user using the software. 
  - An actor can be a human or another system. 
  - Actors are not part of the system; they reside outside the system.
- **Subject**/**System**: The software which is to be built.
- **Preconditions**: Preconditions specify the specific state we expect the system to be in before the use case starts.
- **Guarantees**: Guarantees specify what the use case promises to give us at the end of its operation.
- **Flow of events**: Sequence of steps that describes the interaction between the system and the actors for a particular use case.
  - **Main success scenario (MSS)**: Description of the most straightforward/basic user interaction of the system, assuming that no errors occur.
  - **Extensions**/**Exceptional/alternative flow of events**: Description of variations of the scenario from the MSS, 
  - **Inclusions**: Another use case can be included into a use case. The included use case will be __underlined__, followed by the use case identifier (e.g. `create the survey (UC54)`).

#### Format of a use case
```
Use case: UC01 - Name of Use Case
Actors: List of actors

MSS:
    1. First step
    ...
Steps x-y are repeated until/for each...
    ...
    n. Last step
        Use case ends.

Extensions:
    3a. Description of exception (after Step 3)
        3a1. First step to handle exception
        ...
    Use case resumes from Step x.

    3b. Description of another exception (after Step 3)
        3b1. First step to handle exception
        ...
        Use case ends.
    
    *a. At any time, [description of exception]
        *a1. First step to handle exception
        ...
        Use case ends.
```

#### Use case diagram
**Use case diagrams** help to give an overview of a set of use cases (a kind of a "graphical table of contents" for the use cases).

<img src="images/use-case-diagram.svg" width="500">

### Glossary
A glossary serves to ensure that all stakeholders have a common understanding of the noteworthy terms, abbreviation, acronyms etc.

### Supplementary requirements
A supplementary requirements section contains elements which do not fit elsewhere. The following are a few examples of requirements typically found under this heading.

- **Business/domain rules**: e.g. the size of the minefield cannot be smaller than five.
- **Constraints**: e.g. the system should be backward compatible with data produced by earlier versions of the system; system testers are available only during the last month of the project; the total project cost should not exceed $1.5 million.
- **Technical requirements**: e.g. the system should work on both 32-bit and 64-bit environments.
- **Performance requirements**: e.g. the system should respond within two seconds.
- **Quality requirements**: e.g. the system should be usable by a novice who has never carried out an online purchase.
- **Process requirements**: e.g. the project is expected to adhere to a schedule that delivers a feature set every one month.
- **Notes about project scope**: e.g. the product is not required to handle the printing of reports.
- **Any other noteworthy points**: e.g. the game should not use images deemed offensive to those injured in real mine clearing activities.

## Prioritizing requirements
- **Essential/(must-have)**: The product must have this requirement fulfilled else it does not get user acceptance
- **Typical/(good-to-have)**: Most similar systems have this feature although the product can survive without it.
- **Novel/(nice-to-have)**: New features that could differentiate this product from the rest.

Alternatively, the [MoSCoW Method](https://en.wikipedia.org/wiki/MoSCoW_method):
- Must have
- Should have
- Could have
- Won't have

## Writing better requirements
Here are some characteristics of well-defined requirements:

- Unambiguous
- Testable (verifiable)
- Clear (concise, terse, simple, precise)
- Correct
- Understandable
- Feasible (realistic, possible)
- Independent
- Atomic
- Necessary
- Implementation-free (abstract)
- Consistent
- Non-redundant 
- Complete