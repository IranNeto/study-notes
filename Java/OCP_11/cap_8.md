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

### Calling inherited members

It's possible to call parent members (depending on the access modifier) can be accessed by the `this`.

## Inherit Methods

### Override a Method

**Overriding** a method  occurs when a subclass declares a new implementation for an inherted method
with **the same signature** (Method name and parameters)

To override a method, you must follow:

1 - Method is the child class **must have the same signature** as the parent class
2 - Method in the child class **must NEVER be more restricted** than the parent class
3 - Method in the child class **may not** declare a checked exception that
is new or broader than the class of any exception declared in the parent class method.
4 - Method in the child class **must return the same or a subtype _covariant return types_** of the method in the
parent class

`If two methods have the same name but different signatures, the methods are overloaded, not overriden`

Given an inherited return type A and an overriding return type B, can you assign an instance 
of B to a reference variable for A without a cast? If so, then they are covariant.

## Overriding a Generic Method

### Review of Overloading a Generic Method

Overload means to have the same name and different parameters and/or return type

```java
public class LongTailAnimal {
    protected void chew(List<Object> input) {}
    protected void chew(List<Double> input) {} // DOES NOT COMPILE
}
```

In the example above List is the class type of the parameter, so even if the methods
were in different classes, overloading methods wouldn't work either.

### Overriding generic methods

`you can override a method with generic parameters, but you must match the signature 
including the generic type exactly.`


```java

public class LongTailAnimal {
    protected void chew(List<String> input) {}
}

public class Anteater extends LongTailAnimal { 
    protected void chew(List<String> input) {} //OVERRIDEN
}
```
The example below is not an override operation but a overload operation. Because
the signature is not the same.

```java
public class LongTailAnimal {
    protected void chew(List<Object> input) {}
}
    
public class Anteater extends LongTailAnimal { 
    protected void chew(ArrayList<Double> input) {}
}
```

Java also supports Wildcards

```java
void sing1(List<?> v) {} // unbounded wildcard 
void sing2(List<? super String> v) {} // lower bounded wildcard 
void sing3(List<? extends String> v) {} // upper bounded wildcard
```

### Generic return types

Working with overridden methods that return generics, the return values must be covariant. 
In terms of generics, this means that the return type of the class or interface 
declared in the overriding method must be a subtype of the class defined in the parent class.
The generic parameter type must match its parent’s type exactly.

ReturnType<Generic> - Override - ReturnType must be covariant and Generic must be the same

```java
public class Mammal {
    public List<CharSequence> play() { ... } 
    public CharSequence sleep() { ... }
}
public class Monkey extends Mammal {
    public ArrayList<CharSequence> play() { ... }
}
public class Goat extends Mammal {
    public List<String> play() { ... } // DOES NOT COMPILE 
    public String sleep() { ... }
}
```

## Redeclaring priuvate methods

In Java, you can’t override private methods since they are not inherited.

Java permits you to redeclare a new method in the child class with the same or modified signature
as the method in the parent class.

## Hiding Static Methods

Hidding methods occurs with static members. All the four rules of override a method continues with
one addition

5 - The method defined in the child class must be marked as static if it is marked as static in a parent class.
 
`Put simply, it is method hiding if the two methods are marked static, and method over- riding if they 
are not marked static.`

## Creating final methods

`final methods cannot be replaced`. By marking a method final, you forbid a child class from replacing this method.

## Hiding variables

Java doesn't allow variables to be overriden. Variables can be hidden, though.

A hidden variable occurs when a child class defines a variable with the same name as an inherited variable defined in
parent class. This creates two distinct copies of the variable within an instance of the child class: child and parent
instances

## Object vs. Reference

1. The type of the object determines which properties exist within the object in memory.
2. The type of the reference to the object determines which methods and variables are accessible to the Java program.

### Casting objects

When casting objects, you do not need a cast operator if the current reference is a subtype of the target type.
This is referred to as an implicit cast or type conversion.

1. Casting a reference from a subtype to a supertype doesn’t require an explicit cast.
2. Casting a reference from a supertype to a subtype requires an explicit cast.
3. The compiler disallows casts to an unrelated class.
4. At runtime, an invalid cast of a reference to an unrelated type results in a ClassCastException being thrown.

##The instanceof Operator

instanceof operator, which can be used to
check whether an object belongs to a particular class or interface and to prevent ClassCastExceptions at runtime.

`X instanceof Y`

Just as the compiler does not allow casting an object to unrelated types, it also does not allow instanceof 
to be used with unrelated types. 

## Overriding vs Hiding members

```java
class Penguin {
    public static int getHeight() {
        return 3;
    }

    public void printInfo() {
        System.out.println(this.getHeight());
    }
}

public class CrestedPenguin extends Penguin {
    public static int getHeight() {
        return 8;
    }

    public static void main(String... fish) {
        new CrestedPenguin().printInfo(); //PRINT 3
    }
}
```
Why does it print 3? We're able to call a static method with an instance variable, but the _this_ keyword is related
to a Penguin instance (polymorphic in the CrestedPenguin).

## Summary

1. Overloaded methods must have the same signature?

False, overloaded methods have the same name but can have different parameters or return type

2. Overridden methods must have the same signature? True

3. Hidden methods must have the same signature? True

4. Overloaded methods must have the same return type? False, explained in 2.

5. Overridden methods must have the same return type? True, must have the same name and parameters

6. Hidden methods must have the same return type? True

**PART II**

1. An overridden method must contain method parameters that are the same or covariant with the 
method parameters in the inherited method?

False, it must be the same parameters, different parameters are considered overloaded methods not overriden

2. An overridden method may declare a new exception, provided it is not checked?

False, to override a method is may not declare a new exception or a broader one from the parent method

3. An overridden method must be more accessible than the method in the parent class?

False, an overriden method must be more OR with the same access modifier than the method in the parent class

4. An overridden method may declare a broader checked exception than the method in the parent class?

True, with an broader exception in still comprises the exception declared in the parent method

5. If an inherited method returns void, then the overridden version of the method must
return void?
   
True, void doesn't have a covariant type to be used. So, void can be overriden with a void method

