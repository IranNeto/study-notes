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
