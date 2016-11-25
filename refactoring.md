# CS2103 Lecture 2.2: Refactoring

## Definition
> Improving a program's internal structure without modifying its external behavior.

---

*The following list is the more common refactorings (according to the lecture notes).*

## Consolidate Conditional Expression
- You have a sequence of conditional tests with the same result:
  - Combine them into a single conditional expression and extract it.

```java
// Original:
double disabilityAmount() {
  if (_seniority < 2) return 0;
  if (_monthsDisabled > 12) return 0;
  if (_isPartTime) return 0;
  return computedAmount();
}

// Refactored:
double disabilityAmount() {
  if (isNotEligibleForDisability()) return 0;
  return computedAmount();
}
```

## Decompose Conditional
- You have a complicated conditional (if-then-else) statement.
  - Extract methods from the condition, then part, and else parts.

```java
// Original:
if (date.before (SUMMER_START) || date.after(SUMMER_END)) {
  charge = quantity * _winterRate + _winterServiceCharge;
} else {
  charge = quantity * _summerRate;
}

// Refactored:
if (notSummer(date)) {
  charge = winterCharge(quantity);
} else {
  charge = summerCharge(quantity);
}
```

## Inline Method
- A method's body is just as clear as its name.
  - Put the method's body into the body of its callers and remove the method.

```java
// Original:
int getRating() {
  return (moreThanFiveLateDeliveries()) ? 2 : 1;
}

boolean moreThanFiveLateDeliveries() {
  return _numberOfLateDeliveries > 5;
}

// Refactored:
int getRating() {
  return (_numberOfLateDeliveries > 5) ? 2 : 1;
}
```

## Remove Double Negative
- You have a double negative conditional.
  - Make it a single positive conditional

```java
// Original:
if ( !item.isNotFound() )

// Refactored:
if ( item.isFound() )
```

## Replace Magic Number with Symbolic Constant
- You have a literal number with a particular meaning.
  - Create a constant, name it after the meaning, and replace the number with it.

```java
// Original:
double potentialEnergy(double mass, double height) {
  return mass * height * 9.81;
}

// Refactored:
static final double GRAVITATIONAL_CONSTANT = 9.81;

double potentialEnergy(double mass, double height) {
  return mass * GRAVITATIONAL_CONSTANT * height;
}
```

## Replace Nested Conditional with Guard Clauses
- A method has conditional behavior that does not make clear what the normal path of execution is.
  - Use Guard Clauses for all the special cases.

```java
// Original:
double getPayAmount() {
  double result;
  if (_isDead) result = deadAmount();
  else {
    if (_isSeparated) result = separatedAmount();
    else {
      if (_isRetired) result = retiredAmount();
      else result = normalPayAmount();
    };
  }
  return result;
}

// Refactored:
double getPayAmount() {
  if (_isDead) return deadAmount();
  if (_isSeparated) return separatedAmount();
  if (_isRetired) return retiredAmount();
  return normalPayAmount();
}
```

## Replace Parameter with Explicit Methods
- You have a method that runs different code depending on the values of an enumerated parameter.
  - Create a separate method for each value of the parameter.
```java
// Original:
void setValue(String name, int value) {
  if (name.equals("height")) {
    _height = value;
    return;
  }

  if (name.equals("width")) {
    _width = value;
    return;
  }

  Assert.shouldNeverReachHere();
}

// Refactored:
void setHeight(int arg) {
  _height = arg;
}

void setWidth(int arg) {
  _width = arg;
}
```

## Reverse Conditional
- You have a conditional that would be easier to understand if you reversed its sense.
  - Reverse the sense of the conditional and reorder the conditional's clauses.

```java
// Original:
if ( !isSummer( date ) )
  charge = winterCharge( quantity );
else
  charge = summerCharge( quantity );

// Refactored:
if ( isSummer( date ) )
  charge = summerCharge( quantity );
else
  charge = winterCharge( quantity );
```

## Split Loop
- You have a loop that is doing two things.
  - Duplicate the loop. 

```java
// Original:
void printValues() {
  double averageAge = 0;
  double totalSalary = 0;
  for (int i = 0; i < people.length; i++) {
      averageAge += people[i].age;
      totalSalary += people[i].salary;
  }
  averageAge = averageAge / people.length;
  System.out.println(averageAge);
  System.out.println(totalSalary);
}

// Refactored:
void printValues() {
  double totalSalary = 0;
  for (int i = 0; i < people.length; i++) {
    totalSalary += people[i].salary;
  }

  double averageAge = 0;
  for (int i = 0; i < people.length; i++) {
    averageAge += people[i].age;
  }
  averageAge = averageAge / people.length;

  System.out.println(averageAge);
  System.out.println(totalSalary);
}
```

- N.B. The split loop is an often used performance optimisation in data intensive applications. When you are accessing to separate arrays in the same loop you can get hit badly by the cache misses. 

## Split Temporary Variable
- You have a temporary variable assigned to more than once, but is not a loop variable nor a collecting temporary variable.
  - Make a separate temporary variable for each assignment.

```java
// Original:
double temp = 2 * (_height + _width);
System.out.println (temp);
temp = _height * _width;
System.out.println (temp);

// Refactored:
final double perimeter = 2 * (_height + _width);
System.out.println (perimeter);
final double area = _height * _width;
System.out.println (area);
```

-----

*Content is consolidated from [Refactoring.com by Martin Fowler](http://refactoring.com/catalog).*