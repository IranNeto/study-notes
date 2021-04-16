#Class Design - Inheritance

### Inheritance 
Inheritance is the process by which a subclass automatically includes any 
public or protected members of the class, including primitives, objects, 
or methods, defined in the parent class.

`Inheritance is transitive`

Java supports single inheritance, by which a class may inherit from only 
one direct parent class.

Java does not allow multiple imheritance, EXCEPT when happens with interfaces

`When a class is marked with a final modifier means that it can't be extended
by any class`

## Inheriting Object

Object is the only class that doesn't have a parent class. And all classes created
are already extending java.lang.Object

`toString() and wquals()` are methods present in the Object class. They can
be **overrided** by any class.

Primitive types such as int and boolean do not inherit from Object, since they 
are not classes.

## Extending a class

[access modifier][abstract/final] class [class name][extends][parent class] {}

## Applying Class Access Modifiers

It's possible to apply access modifiers to class definition.

`top-level class is a class that is not definied inside another class`

* Public class: Applying public modifier means that it can be referenced
by any class.
* Default class: Package-private or default modifier is the lack of any modifier
and indicates that the class can be accessed only by a class within the same package
* Private classes: It can exists only inside other class as an field (Inner class)

`Inner class is a class defined inside a top-level class`

**Java must have only one public class, no matter how many top-level class**

**A public class has to be inside a java file with its name**

## Accessing "this" reference

The this reference refers to the current instance of the class. Can be used
to get any member of the class _including inherited methods_

**this cannot be used to static methods/fields**

Java always look first to the smaller scope

If Java encounters a variable or method it cannot find, it will check the class 
hierarchy to see if it is available.

## Calling the "super" reference

_super_ is very similar to _this_ except by the fact that it excludes the actual
instance methods/fields. It only accesses the pareents members accessible by inheritance.

## Creating a Constructor

Constructor is a special method that **has no return type**. 

[Acess modifier][Class name][(parameters)]{}

A class can have multiple constructors, so long as it may have multiple signatures

**Constructor overloading** happens when we have multiple constructors that differs 
on the method signature

The method name and parameter types are called the **method signature**.

## Default constructor

Every class has a default constructor - it has no args. Even if we don't include this, Java
generate it in compile time (look at .class).

Having only private constructors in a class tells the compiler not to provide 
a default no-argument constructor.

## Calling overloaded constructors with "this"

Constructors can be called only by writing new before the name of the constructor.

```java
public class Hamster{
    Hamster(int x, String y){}

    Hamster(int x){
        Hamster(x, "default"); //DOES NOT COMPILE
        new Hamster(x, "default"); //COMPILES, but does nothing
        this(x, "default") // <- COMPILES, correct option
    }
}
```

**IMPORTANT**

1 - `this(...) or super(...) MUST BE the first instruction inside the constructor`

2 - `It MUST exists only one this(...) or super(...) by constructor`

3 - `The compiler is capable of know when a infinite recursion with constructors exists = COMPILE ERROR`

## Understand compuiler enhancements

Java compiler automatically inserts a call to the no-argument constructor 
super() if you do not explicitly call this() or super() as the first line of a constructor.
No-argument constructor is not required and is inserted by the compiler 
**only if there is no constructor defined in the class**.

A class that only has private constructors and is not final can be extended only by a inner class
defined in the class itself. This way it is going to have access to the private methods.

```java
public class Mammal {
    public Mammal(int age) {}
}
public class Elephant extends Mammal {} // DOES NOT COMPILE

```

Let's see what's happening

1 - In compile time, the compiler will generate a default no-args constructor to Elephant class.

2 - First, it'll call `super()` once we are extending Mammal.

3 - Mammal is not defining a no-args constructor, so compiler cant't create an Elephant constructor
and therefore, we get a compiler error.

```java
public class Elephant extends Mammal {
    public Elephant() {
        super(); // DOES NOT COMPILE 
    }
}
```

Since the Mammal class has at least one constructor declared, the compiler does not insert 
a default no-argument constructor.

`Subclasses may define explicit no-argument constructors even if their parent classes do not, 
provided the constructor of the child maps to a parent constructor via an explicit call of the
 super() command. This means that subclasses of the Elephant can rely on compiler enhancements.`

## Constructor and final fields

Final instances variables MUST be assigned a value. It can happen in the declaration itself
in a context block or inside the constructor.

Constructor as the last step of initialization must assure that in every possible situation
the final fields will be initialized.

The compiler reports this error on the line where the field is set. Not at the declaration

## Order of initialization
### Class Initialization

`LOADING THE CLASS`
A class must be initialized before it is referenced or used.
First start with all static members. Starting from the highest parent to the current class. 

1 - All the parents should initialize from up to bottom.
2 - All static variable declaration happens in the order as they appear.
3 - ASll static initializers in the order they appear.

### Instance Initialization

An instance is initialized anytime the new keyword is used.

1 - All the parents should initialize from up to bottom
2 - All instance variable declaration in the order as they appear
3 - All initializers in the order as they appear
4 - Initialize the constructor, including any overloaded constructors referenced with this()

## Constructor rules

1 - The first statement of every constructor is a call to an overloaded constructor via this(), 
or a direct parent constructor via super().

2 - If the first statement of a constructor is not a call to this() or super(), then the 
compiler will insert a no-argument super() as the first statement of the constructor.
**IF the parent has a no arg constructor defined, not only an arg constructor instead**.

3 - Calling this() and super() after the first statement of a constructor results in a 
compiler error.

4 - If the parent class doesn’t have a no-argument constructor, then every constructor 
in the child class must start with an explicit this() or super() constructor call.

5 - If the parent class doesn’t have a no-argument constructor and the child doesn’t 
define any constructors, then the child class will not compile.

6 - If a class only defines private constructors, then it cannot be extended by a top-level class.

7 - All final instance variables must be assigned a value exactly once by the end of the
constructor. Any final instance variables not 
assigned a value will be reported as a compiler error **on the line the constructor is declared.**

## Inherit Members