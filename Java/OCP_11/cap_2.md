# Working With Java Primitive Data Types and String APIs

## Constructors
```java
//Creating a new Object
Chick chick = new Chick();

public class Chick {
    //No parameter constructor 
    public Chick() {
        System.out.println("in constructor"); 
    }

    public void Chick() { } // NOT A CONSTRUCTOR
}
```

**The name of the constructor match the class name and there's no return type**

Constructors are for initialize instance variables but they also can be initialized in the declaration.

```java
public class Chicken {
    int numEggs = 12; // initialize on line String name;

    public Chicken() {
        name = "Duke"; // initialize in constructor 
    }

}   
```

It’s possible to read and write instance variables directly from the caller.

## Executing Instance Initializer Blocks
braces {} means a scope for a code block. Some of them can be found inside of a method. When finding braces is important to pat attention in 2 things:

* All open braces are close with a close brace (number of open braces == number of close braces)
* variables'scopes

### Order of initialization

* Fields and instance initializer blocks are run **in the order** in which they appear in the file.
    ```java
    public class Chick {

        { //This is an ilegal forward reference and gets a COMPILATION ERROR
            //System.out.println(name)
        }

        private String name = "Fluffy"; //1 - Variable setted

        {
            System.out.println(name); //2 - prints Fluffy
            System.out.println("setting field"); //3 - prints it
        }

        public Chick() {
            System.out.println(name); //4 - prints Fluffy
            name = "Tiny";
            System.out.println("setting constructor"); //5 - prints it
        }

        public static void main(String[] args) {
            Chick chick = new Chick(); //0 - Creates an object
            System.out.println(chick.name); //6 - prints Tiny
        }
    }

    ```

`Pay attention to illegals forward reference.`

## Understanding Data Types

Java applications contain two types of data: primitive types and reference types.

### Primitive types

A primitive is not an object in Java nor does it represent an object. A primitive is just a single value in memory, such as a number or character.

| Keyword | Type                  | Example |
|---------|-----------------------|---------|
| boolean | `true` or `false`     | `true`  |
| byte    | 8-bit                 | 123     |
| char    | 16-bit Unicode        | 'a'     |
| short   | 16-bit                | 123     |
| int     | 32-bit                | 1234    |
| long    | 64-bit                | 1234L   |
| float   | 32-bit floating-point | 12.12f  |
| double  | 64-bit floating-point | 123.3   |

Observations:

* **String is not a primitive**
* All of the numeric types are **signed** in Java
* char is nor signed
* short and char are close related having the same size
* float and double are not close related

### Writing literals

**By default, Java assumes you are defining an int value with a numeric literal.**

Below, the number is bigger than an integer support even if the variable we are trying to initialize is a long typed. 

```java
long max = 3123456789; // DOES NOT COMPILE
```
To fix that, we're supposed to put an L after the number to indicate a long value.

```java
long max = 3123456789L; // now Java knows it is a long
```

Another way to specify numbers is to change the base. Java accepts different bases: Binary, octal, decimal, hexadecimal.

```java
long a = 0xBA2C2B15A; //COMPILATION ERROR - Number too large 
long a = 0xBA2C2B15AL; //Now works
```

### Literals and the Underscore Character

You can add underscores anywhere to improve readability except:
* At the beginning of a literal
* The end of a literal
* Right before or after the decimal point.

```java
double notAtStart = _1000.00; // DOES NOT COMPILE
double notAtEnd = 1000.00_; // DOES NOT COMPILE
double notByDecimal = 1000_.00; // DOES NOT COMPILE
double annoyingButLegal = 1_00_0.0_0; // Ugly, but compiles
double reallyUgly = 1__________2; // Ugly, but compiles
```

## Using Reference Types
A reference type refers to an object (an instance of a class). Unlike primitive types that
hold their values in the memory where the variable is allocated, **references do not hold the value of the object they refer to**.

```java
java.util.Date today = new java.util.Date();
String greeting = new String("Hey you");
```

`today`is a java.util.Date reference and can only reference to it. `greeting`is a String reference to an String object and can only reference String.

* A reference can be assigned to another object of the same or compatible type.
* A reference can be assigned to a new object using the new keyword.

### Reference vs Primitives

1 - References types can be assigned to _null_. `null` means that we're not referencing to an object.
2 - Reference types can be used to call method _assuming the reference is not null_. If we try to call a method or attribute by a null reference we get a `NullPointerException`.


## Variables

### Declaring variables

```java
//Type variableName = new Object() or primitive_value

//Just declaration
String zooName;
int numberAnimals;

// initializing
zooName = "The Best Zoo"; 
numberAnimals = 100;

//Declaration and initialization
String zooName = "The Best Zoo";
int numberAnimals = 100;
```

### Variable names

An identifier is the name of a variable, method, class, interface, or package.

There are only 4 rules to remember for legal identifiers

* Identifiers must begin with a letter, a $ symbol, or a _ symbol. 
* Identifiers can include numbers **but not start with them**.
* Since Java 9, **a single underscore _ is not allowed** as an identifier.
* You cannot use the same name as a Java **reserved word**. 

```java
//VALID
long okidentifier;
float $OK2Identifier;
boolean _alsoOK1d3ntifi3r;
char __SStillOkbutKnotsonice$;

//INVALID
int 3DPointClass; // identifiers cannot begin with a number 
byte hollywood@vine; // @ is not a letter, digit, $ or _ 
String *$coffee; // * is not a letter, digit, $ or _ 
double public; // public is a reserved word
short _ ; // a single underscore is not allowed
```

### Declaring Multiple Variables

 You can declare many variables in the same declaration as long as they are all of the **same type**.

 ```java
void sandFence() {
    //Only it is initialized - i0 and i1 are just declared
    int i0, i1, it = 0;
    String s1, s2;
    String s3 = "yes", s4 = "no";

    int num, String value; // DOES NOT COMPILE
    double d1, double d2; // DOES NOT COMPILE
    int i1; int i2; // LEGAL - There's a semicolon between them
    int i3; i4; // DOES NOT COMPILE

}
 ```

 ### Initializing Variables

Before you can use a variable, it needs a value. A local variable is a variable defined within a constructor, method, or initializer block.

```java
public int notValid() { 
    int y = 10;
    int x;
    int reply = x + y; // DOES NOT COMPILE 
    return reply;
}

public int notValid() { 
    int y = 10;
    int x;
    x = 1;
    int reply = x + y; // COMPILE 
    return reply;
}
```
The compiler is also smart enough to recognize initializations that are more complex.

```java
public void findAnswer(boolean check) { 
    int answer;
    int otherAnswer; 
    int onlyOneBranch; 
    
    if (check) {
        onlyOneBranch = 1;
        answer = 1; 
    } else {
        answer = 2; 
    }
    
    System.out.println(answer);
    System.out.println(onlyOneBranch); // DOES NOT COMPILE 
}
```
**Remember, the compiler is only concerned if you try to use uninitialized local variables; it doesn’t mind the ones you never use.**

### Passing Constructor and Method Parameters

To pass a variable through some constructor or method it should be initialized before passing.

```java
public void findAnswer(boolean check) {}

public void checkAnswer() {
    boolean value;
    findAnswer(value); // DOES NOT COMPILE
}
```
### Instance and Class Variable

An instance variable, often called a field, is a value defined within a specific instance of an object. A class variable is one that is defined on the class level and shared among all instances of the class. You can tell a vari- able is a class variable because it has the keyword `static` before it.

Instance and class variables do not require you to initialize them. They are initialized with a default value.

| Variable Type | Default value |
|---------|--------------- |
| boolean | `false`       |
| byte    | 0             |
| char    | '\u0000' (NUL)|
| short   | 0   |
| int     | 0   |
| long    | 0   |
| float   | 0.0 |
| double  | 0.0 |
| Objects | null |

## The local variable type inference (var)

Starting in Java 10, you have the option of using the keyword var instead of the type for local variables under certain conditions.

```java
class Test{
    var s = "tricky"; //DOES NOT COMPILE

    public void whatTypeAmI() { 
        var name = "Hello"; //String
        var size = 7; //int
    }

    public void varNotAParameter(var s){} //DOES NOT COMPILE
}
```

Local variable type inference works with local variables and not instance variables.

Local variables declared with var have its type defined in **Compile time**, so, they cannot be reassigned to another type in **Run time**.


```java
class Test{
    public void whatTypeAmI() { 
        var name = "Hello"; //String
        name = "Hi";
        name = 7; //DOES NOT COMPILE
    }
}
```

Local variables with *var* must be assigned after declared

```java
class Test{
    public void whatTypeAmI() { 
        var name = "Hello"; //String
        var x; //DOES NOT COMPILE
        
        var y
            = 1L; //long
    }
}
```

**Java does not allow var in multiple variable declarations.**

Java does not accept var s = null because `null` value can be refered to any Object type. But it's possible to reassign `var` variable to `null` after it's assigned to any reference Object type.
```java
class Test{
    public void whatTypeAmI() { 
        int a, var b = 3; // DOES NOT COMPILE

        var n = null; // DOES NOT COMPILE
        var o = (String)null;

        var m = 1;
        m = null; //DOES NOT COMPILE - primitive int cannot be null

        var x = "String";
        x = null;
    }
}
```

**`var` isn't a reserved word**. `var` is considered a reserved type name. A reserved type name means **it cannot be used to define a type, such as a class, interface, or enum**

```java
public class Var { 
    public void var() { 
        var var = "var";
    }
    
    public void Var() {
        Var var = new Var(); 
    }
}
```

```java
public class var { // DOES NOT COMPILE 
    public var() {}
}
```

### Review of var Rules
1. A var is used as a local variable in a constructor, method, or initializer block.
2. A var cannot be used in constructor parameters, method parameters, instance vari- ables, or class variables.
3. A var is always initialized on the same line (or statement) where it is declared.
4. The value of a var can change, but the type cannot.
5. A var cannot be initialized with a null value without a type.
6. A var is not permitted in a multiple-variable declaration.
7. A var is a reserved type name but not a reserved word, meaning it can be used as an identifier except as a class, interface, or enum name.

## Variable Scope

Variable declared in larger scopes can be accessed in inner nested scopes.

```java
public void eatIfHungry(boolean hungry) { 
    
    if (hungry) {
        int bitesOfCheese = 1;
    } // bitesOfCheese goes out of scope here
    
    System.out.println(bitesOfCheese); // DOES NOT COMPILE
}
```

```java
public void eatIfHungry(boolean hungry) { 
    if (hungry) {
        int bitesOfCheese = 1; 
        {
            var teenyBit = true;
            System.out.println(bitesOfCheese); 
        }
    }
    System.out.println(teenyBit); // DOES NOT COMPILE }
```

* Local variables: In scope from declaration to end of block
* Instance variables: In scope from declaration until object eligible for garbage collection
* Class variables: In scope from declaration until program ends

## Garbage Collection

JVM automatically takes care of object destruction. **Garbage collection** refers to the process of automatically freeing memory on the heap by deleting objects that are no longer reachable in your program.

All Java objects are stored in your program memory’s heap. The heap, which is also referred to as the free store, represents a large pool of unused memory allocated to your Java application.

There’s very little you can do to control garbage collection directly in Java.

In Java and other languages, eligible for garbage collection refers to an object’s state of no longer being accessible in a program and therefore able to be garbage collected.

* Does this mean an object that’s eligible for garbage collection will be immediately garbage collected? 
  * Definitely not.

Java includes a built-in method to help support garbage collection that can be called at
any time.

```java
public static void main(String[] args) { 
    System.gc();
}
```

* What is the `System.gc()` command guaranteed to do? 
  * **Nothing,** actually. It merely *suggests* that the JVM kick off garbage collection. 

* When is System.gc() guaranteed to be called by the JVM? 
    * **Never**, actually.

### Tracing Eligibility for GC

1. The object no longer has any references pointing to it. 
2. All references to the object have gone out of scope.
3. It is the object that gets garbage collected, not its reference.

# Important Notes from exercises

```
* String has a .lenght()
* A local variable cannot receive a default number. Try to use a local variable without assinging to it a value generates a COMPILE ERROR
* 
```
