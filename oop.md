# CS2103: Object-Oriented Programming (OOP) Concepts

## Encapsulation
An object is an encapsulation of some data and related functions.

1. It *packages* those data and related functions together into one entity.
2. The data is hidden from the outside world (**information hiding**) and are only accessible using the functions.

## Exceptions
> An exception is an event, which occurs during the execution of a program, that disrupts the normal flow of the program's instructions.

- Most languages allow a method to encapsulate the unusual situation in an Exception object and ‘throw’ that object so that another piece of code can ‘catch’ it and deal with it. Usually, an exception thrown by a method is caught by the caller method. 
- If the called method does not know how to deal with the exception it caught, it will throw the Exception object to its own caller. 
- If none of the callers is prepared to deal with the exception, the exceptions can propagate through the method call stack until it is received by the main method and thrown to the runtime, thus halting the system.

## Inheritance
Applying the concept of **inheritance** can result in the common parts among classes being extracted into more general classes. Inheritance implies the derived class can be considered as a sub-type of the base class (and the base class is a super-type of the derived class), resulting in an ‘is a’ relationship.

Every instance of a subclass is an instance of the superclass, but not vice-versa. Inheritance allows **substitutability** - wherever an object of the superclass is expected, it can substituted by an object of any of its subclasses.

## Interfaces
In an OO solution, an interface is a behavior specification. In Java, a class can be explicitly declared as an interface which can then be used to specify the available operations without implementing any. If a class implements all operations specified in an interface, it is said that the class ‘implements’ the interface.

In UML, an interface is depicted with the keyword `<<interface>>`.

## Abstract classes/methods
An **abstract method** is a method definition that does not have a body. A class containing at least one abstract method is called an **abstract class**. In this context, abstract means 'not fully specified'.

An abstract class cannot be instantiated, as it is considered incomplete. Only classes which implement all of the abstract methods can be instantiated; otherwise it is also an abstract class. Furthermore, some OOP languages allow declaring a class as abstract even if it does not have any abstract operations so as to prevent it from being instantiated.

In UML, an abstract class or method is depicted with the keyword `{abstract}`, as follows:

![](images/abstract-classes-methods.svg)

## Polymorphism
> Polymorphism is the ability to treat objects of different types in a similar manner.

Hence, inheritance allows polymorphism, as subclasses inherit superclass methods, and we can then invoke superclass methods on the instance of the subclass, as if it were an instance of the superclass.

### Operation overriding
By **overriding** methods from superclasses in the subclasses, we can achieve polymorphic behaviour. This is resolved at runtime (as compared to method overloading, which is resolved at compile-time), using **dynamic binding** (as compared to *static binding*) which will bind the actual method definition to the invocation of the method. If the subclass has overridden the method in question, the overriden method will be called, otherwise it will fallback on the superclass method definition.

### Multiple inheritance
Multiple inheritance of classes is allowed in C++ but not in Java, however it allows for a class to implement multiple interfaces.

### Downcasting in Java
Downcasting refers to casting an object to one of the subclasses of its type. Typically will either cause a compile-time error or a runtime error (`ClassCastException`), if the object is not actually an instance of the subclass.

The following are some examples:

```java
Object o = getSomeObject(),
String s = (String) o; // this is allowed because o could reference a String

Object o = new Object();
String s = (String) o; // this will fail at runtime, because o doesn't reference a String

Object o = "a String";
String s = (String) o; // this will work, since o references a String

Integer i = getSomeInteger();
String s = (String) i; // the compiler will not allow this, since i can never reference a String.
```

## Coupling
Coupling is a measure of the **degree of dependence between components, classes, methods, etc**. Low coupling indicates that a component is less dependent on other components. In the case of high-coupling (i.e. relatively high dependency), a change in one component may require changes in other coupled components. Therefore, one should strive to achieve a low-coupled design.

### Disadvantages of highly-coupled design
- A change in one module usually forces changes in other modules coupled to it (i.e. a ripple effect).
- Integration is harder because multiple components coupled with each other have to be integrated at the same time.
- Testing and reuse of the module is harder due to its dependence on other modules.

## Cohesion
Cohesion is a measure of **how strongly-related and focused the various responsibilities of a component are**. A highly-cohesive component keeps related functionalities together while keeping out all other unrelated things. One should strive for high cohesion to facilitate code maintenance and reuse.

Cohesion comes in multiple forms:

- Code related to a single concept is kept together in the same file/location
- Code that is invoked close together in time is kept together (e.g. sequentially ordered methods)
- Code that manipulates the same data structure is kept together

### Disadvantages of low-coupled design
- Impedes the understandability of modules as it is difficult to express module functionalities at a higher level.
- Difficulty in maintaining modules because a localized adjustment in the requirements can result in changes spread across the system since requirement-related functionality is implemented across many components of the system.
- Modules become less reusable because they do not represent logical units of functionality.