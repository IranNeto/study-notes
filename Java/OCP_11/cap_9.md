# Advanced Class Design

## Abstract classes

An abstract class is a class that acnnot be instantiated and may contain
abstract methods (methods that does not define an implementation when it is 
declared).

Abstract methods inherited are mandatory to be implemented by the Child class.

An abstract class is most commonly used when you want another class to 
inherit properties of a particular class, but you want the subclass to fill
in some of the implementation details.

**When implementing (overriding is the best word) an abstract method the rules
for overriding are yet applicable**.

`An abstract class can be initialized, but only as part of the
instantiation of a nonabstract subclass.`

Abstract classes cannot be instantiated but can have multiple constructors.

`Abstract methods can only be defined in an abstract class`

Like the final modifier, the abstract modifier can be placed before or
after the access modifier in class and method declaration.

```java
abstract public class Tiger { 
    abstract public int claw();
}
```

Abstract methods cannot be final because they are not going to be overrided

### Constructor in Abstract Classes

`Constructor rules are still valid for abstract classes`

For example, if an abstract class does not provide a constructor,
the compiler will automatically insert a default no argument constructor.

The primary difference between a constructor in an abstract class and a
nonabstract class is that a constructor in abstract class can be called only
when it is being initialized by a nonabstract subclass.

### Invalid abstract method declarations and modifiers

```java
public abstract class Turtle {
    //NONE COMPILES 
    public abstract long eat() 
    public abstract void swim() {}; 
    public abstract int getAge() { return 10; }
    public void sleep;
    public void goInShell();
}
```

### Invalid modifiers

1. Java does not permit a class or method to be marked both abstract and final.

2. A method cannot be marked as both abstract and private. How would you define
a subclass that implements a required method if the method is not inherited by
the subclass?

3. A method cannot be marked as both static and abstract. Static methods are hidden
not overridden since it does not belong to the instance but to the class.

## Creating a concrete class

**The first concrete subclass that extends an abstract class is required to 
implement all inherited abstract methods**. It must be the first.

```java

abstract class Mammal { 
    abstract void showHorn();
    abstract void eatLeaf();
}

abstract class Rhino extends Mammal { 
    void showHorn() {} //OVERRIDED and IMPLEMENTED
}

public class BlackRhino extends Rhino { 
    //BlackRhino extend a non abstract showHorn once Rhino class has
    //implemented it
    void eatLeaf() {}
}
```

By changing Rhino to a concrete class, it becomes the first 
nonabstract class to extend the abstract Mammal class. Therefore, it must 
provide an implementation of both the showHorn() and eatLeaf() methods.

## Abstract class and method summary

1. Abstract classes cannot be instantiated.
2. All top-level types, including abstract classes, cannot be marked protected
or private.
3. Abstract classes cannot be marked final.
4. Abstract classes may include zero or more abstract and nonabstract methods.
5. An abstract class that extends another abstract class inherits all of
its abstract methods.
6. The first concrete class that extends an abstract class must provide an
implementation for all of the inherited abstract methods non implemented.
7. Abstract class constructors follow the same rules for initialization as
regular constructors, except they can be called only as part of the
initialization of a subclass.

## Interfaces

An interface is defined with the interface keyword, analogous to the class kwyword.

[access modifier][implicit abstract][interface][Interface name] {
    Float getSpeed(int age);
    int MINIMUM_DEPTH = 2;
}

In interfaces we have implicit modifiers

1. Every method **without a body** inside an interface is public and abstract by nature
2. Every interface variable is public, static and final by nature.

Interfaces does not requre to define any methods.

Interfaces cannot be instantiated.

Interfaces cannot be marked as final

### Implementing an interface
```
[access modifier][class][Class name][implements][InterfaceName1, InterfaceName...]{

    [public (required)][Covariant return type][same method name][same parameters]{
    
        ...
        
    }
    
}
```

**An interface extends another interface, not implement it**.

Unlike abstract classes, they do not contain constructors and are not part of instance
initialization. Interfaces simply define a set of rules that a class
implementing them must follow. 

A top-level class or interface can only be declared with public or
package-private access.

### Conflicting modifiers

If a developer marks a method or variable with a modifier that conflicts with an
implicit modifier the code **does not compiles**.

REMEMBER: Not marking with any access modifier inside an interface the compiles
will automatically set up with public final or static it it's a method or
an instance variable.

### Differences between interfaces and abstract classes

 When a concrete class implements an interface it must be sure that the overriden methods
 are marked as public, since it is implicitly public in the interface.
 
### Intheriting an interface

* An interface can extend another interface.
* A class can implement an interface.
* A class can extend another class whose ancestor implements an interface.

An interface cannot be extend, just implemented. Also, an interface cannot extend a class.

### Duplicate interface method declaration

What would happen with a class 2 interfaces with the same method
signature?

As they having identical method declaration, it would be *compatible*.

If two abstract interface methods have identical behaviors—or in
this case the same method declaration—you just need to be able to create
a single method that overrides both inherited abstract methods at the same
time.

If the methods have different method signatures and same return type,
then the methods are overloaded
and the class who implements it must implement all the methods.

If the methods have the same signature but different return types than
it must be analysed if they are covariant, if it is, then the class must
implement that with the **smaller scope** to be compliant with the method
with broader return type.

The compiler would also throw an exception if you define an abstract
class or interface that inherits from two conflicting abstract types.

## Polymorphism and interfaces

When working with abstract types, you may prefer to work with the
abstract reference types, rather than the concrete class.

Why? It's easier to not depend on a class implementation. We rely on an interface
that have an specific method that we use. Therefore, any instance that is covariant
of the interface will be able to perform the same instruction. It can be used interchangeably
and it is compliant with the Liskov Substitute Principle from SOLID.

### Casting interfaces

```java
interface Canine {}

class Dog implements Canine {} class Wolf implements Canine {}

public class BadCasts {
    public static void main(String[] args) {
        Canine canine = new Wolf();
        Canine badDog = (Dog)canine; 
    } 
}
```

#### Interface limitation
In the example above, the code compiles. . Because of polymorphism, Java cannot be
sure which specific class type the canine instance. Therefore, it allows the invalid
cast to the Dog reference, even when they are not related. So code throws a
ClassCastException at runtime.

The compiler does not allow a cast from an interface reference to an object reference
if the object type does not implement the interface.

### Interfaces and the instanceof Operator

With interfaces, the compiler has limited ability to enforce this rule because even
though a reference type may not implement an interface, one of its subclasses could.
```java

Number tickets = 5;
if(tickets instanceof List) {}
if(tickets instanceof String) {} // DOES NOT COMPILE

```

In this case `tickets instanceof List` compiles because the compile can be sure that
tickets may be a Number sublass that implements List. 

````java
public class MyNumber extends Number implements List{}
````

Even though, the code throw a ClassCastException.

the compiler can check for unrelated interfaces if the reference is
a class that is marked final.

```java
Integer tickets = 6;
if(tickets instanceof List) {} // DOES NOT COMPILE
```

The compiler rejects this code because the Integer class is marked
final and does not inherit List. Therefore, it is not possible to create
a subclass of Integer that inherits the List interface.

## Summary

### Interface definition

1. Interfaces cannot be instantiated.
2. All top-level types, including interfaces, cannot be marked
protected or private.
3. Interfaces are assumed to be abstract and cannot be marked final.
4. Interfaces may include zero or more abstract methods.
5. An interface can extend any number of interfaces.
6. An interface reference may be cast to any reference that inherits
the interface, although this may produce an exception at runtime if the 
lasses aren’t related.
7. The compiler will only report an unrelated type error for an
instanceof operation with an interface on the right side if the
reference on the left side is a final class that does not inherit
the interface.

### Abstract Interface Method

1. Abstract methods can be defined only in abstract classes or interfaces.
2. Abstract methods cannot be declared private or final.
3. Abstract methods must not provide a method body/implementation
in the abstract class in which is it declared.
4. Implementing an abstract method in a subclass follows the same
rules for overriding a method, including covariant return types, exception
declarations, etc.
5. Interface methods without a body are assumed to be abstract and public.

### Interface variables

1. Interface variables are assumed to be public, static, and final.
2. Because interface variables are marked final, they must be initialized
with a value when they are declared.

## Inner classes

A member inner class is a class defined at the member level of a class
(the same level as the methods, instance variables, and constructors).

A member inner class can contain many of the same methods and variables
as a top-level class. Some members are disallowed in member inner classes,
such as static members.

1 - 