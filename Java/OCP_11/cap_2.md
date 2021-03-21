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
String *$coffee; // * is not a letter, digit, $ or _ double public; // public is a reserved word
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

