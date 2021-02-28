# Single Responsibility Principle - SRP

`cohesive code` `spread of change`

A class should have one, and only one, purpose

**What is a cohesive code?**

A cohesive code is a piece of a project (class, module, etc) that has only one purpose and is self-contained. Self-contained
means that his functionalities aren't spread throughout the project but is contained only inside of it. SRP helps to developers
stick with a cohesive code during its growth or maintain times. A cohesive code follows DRY.

**What is a coupled code and why SRP decouple it?**

Let's consider a class. Classes should be as independent as possible from other classes, so that changes to class don’t 
heavily impact other classes. High coupling would mean that your class knows the way too much about the inner workings 
of other class. If class A knows too much about class B, changes to the internals of class B may break functionality in class A.
The spread of change is way bigger and has more impact when a code is tight coupled and it becomes harder to do any change on it.

Classes are align with SRP when
* Stop growing indefinitely
* Not constantly modified
* Reusable

Benefits
* Code easy to read, maintain and test
* Decrease coupling
* Class cohesiveness

Using ctrl+F or search tool a lot when some change is required is a sign that it's not a good OO code.

`Change points must be explicity in code design`

