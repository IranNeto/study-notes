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

