### 1. What are the SOLID Principles?

SOLID Principles is an acronym of 5 principles in Object Oriented Design (OOD). Robert C. Martin introduced these 5 principles in his 2000 paper "Design Principles and Design Patterns".

S - Single Responsibility Principle
O - Open Closed Principle
L - Liskov Substitution Principle
I - Interface Segregation Principle
D - Dependency Inversion Principle
1. Describe the Single Responsibility Principle (SRP).

In Object Oriented Programming, Single Responsibility (SRP) ensures that every module or class should be responsible for single functionality supported by the software system. In other words, Every class should have one and only reason to change it.
For example, In ASP.NET MVC HomeController class should be responsible related to Home Page functionality of software system.


 
### 3. Describe the Open Close Principle (OCP).

Open Close Principle (OCP) states or ensures that A class, component or entity should be open for extension but close for modification. In detail, We can extend any class via Interface, Inheritance or Composition whenever it's required instead of opening a class and modifying it's code.
For example, suppose you have implemented a functionality to calculate area of Rectangle and after some time you need to calculate the area of Square, then In this case you should not modify your original class code to add extra code for square. Instead you should create one base class initially and now you should extend this base class by your square class.

### 4. Explain Liskov Substitution Principle (LSP).

Liskov Substitution Principle (LSP) states that Objects in a program can be replaced by the instances of their subtypes without modifying the correctness of a program.
In other words, if A is subtype of B then instances of B may be replaced by the instances of A without altering the program correctness.

### 5. Explain Interface Segregation Principle (ISP).

Interface Segregation Principle (ISP) states that use many client specific interfaces instead of one general purpose interface.
In other words No client should be forced to implement other methods which it does not require. It means it's better to create a separate interface and allow your classes to implement multiple interfaces.

### Explain DIP(dependancy Inversion)
The Dependency Inversion Principle (DIP) states that high level modules should not depend on low level modules; both should depend on abstractions. Abstractions should not depend on details. Details should depend upon abstractions.

