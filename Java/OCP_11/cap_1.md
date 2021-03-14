# Understand Java technology and environment basics

## Benefits of Java
    Object Oriented
        
        All code is defined in classes and most of those classes can be instantiated into objects

    Encapsulation
        Support to access modifiers to protect data from uninteded access and modification

    Platform Independent
        Java is and interpreted language that gets compile to bytecode. Once compliled there's no needing to recompile for differentes operationg sustems. Portability.
        "Write once, run everywhere"

    Roubust
        Prevents memory leaks through garbage collection automatically

    Simple
        No pointers or operator overloading compared to C++

    Secure
        Jaca tuns inside the JVM that creates a sandbox making it hard for Java code to do eveil things to the computer it's running on.
    
    Multithreaded

    Backward Compatibility
        When a code is going to disapear in new Java versions it's marked as deprecated, so the devs are able to change it.

## Java Components
    
Java Development Kit (JDK) - Minimum software you need to do Java development. Inside it:

*  **javac** (compiler) that transform .java in .class (with code in bytecode)
*  the launcher **java** which creates the VM and execute the programs
*  **jar** command to package files together
*  **javadoc** command for generating documentation

**JRE is not present starting from Java 11** - JRE was a JDK subset just to run programs not to compile it.

## Java class structure

* **object** is a runtime instace of a class in memory
* A **reference** is a variable that points to an object

```java
public class Animal {
    String name;

    public String getName() {
        return name;
    }
    
    public void setName(String newName) {
         name = newName;
    }
}
```

The method name and parameter types are **method signature**
```java 
public void setName(String newName)
```

## Comments

```java 
// comment until end of line

/* Multiple
* line comment 
*/

2 stars on the beginning

/**
* Javadoc multiple-line comment 
* @author Jeanne and Scott
*/

```

Compiler always look to a /* that closes with a */ no mattering what are in between

## Classes vs. Files

You can even put two classes in the same file. When you do so, at most one of the classes in the file is allowed to be public. Also 

**If you do have a public class, it needs to match the filename.**

```java
//Animal.java
public class Animal {
    private String name;
}

class Animal2 {}
```

## Executing Java Program

### Main method

A java program executes with the main method. 

```bash
javac -version #compiler version
java -version #laucher version
```

A main methd has a mandatory method signature

```java
public class Zoo {
    public static void main(String[] args) {
        System.out.println("Welcome!");
    }
}
```

```bash
javac Zoo.java #compile the .java in .class
java Zoo #execute the program
```

Alternatives to main method signature

```java
public static void main(String[] args)
public static void main(String... args)
public static void main(String args[])
```

**The name of the parameter is no important** and could be anything.

### Passing parameters to main method

Main method will interpret and count the words passed by parameter. So if it's passed "San Diego" we'd have a two elements String array [San, Diego]. 

**The parameter is parsed by space character**

**Or to an expression be parsed as an array element it should be between "".**

```java
public class Zoo {
    public static void main(String[] args) {
        System.out.println(args[0]);
        System.out.println(args[1]); 
    }
}
```

```bash
javac Zoo.java
java Zoo San Diego

San
Diego

javac Zoo.java
java Zoo San "San Diego" San

San
San Diego
```

### One line run - single-file source-code programs
Starting from java 11

```bash
java Zoo.java San Diego

San
Diego
```

Rules:
* One file program
* One class only
* Can’t refer to any .class files that didn’t come with the JDK.

**Instead of compiling into a .class file it's done "in memory"**

| Full command        |  Single-file source-code-command                                      |
|-----------------------------------------------|:-------------------------------------------:|
| javac HelloWorld.java && java HelloWorld |            java HelloWorld.java                  |
| Produces a class file                    |              Fully in memory                     |
| For any program                          |        For programs with one                     |
| Can import code in any available Java library | Can only import code that came with the JDK |

## Package declaration and Imports

```java
package br.com.example; //1 - package declaration - optional

import java.util.*; //2 - import libraries - optional
import java.lang.*;

public class ImportExample { //class declaration - mandatory
    public static void main(String[] args) { 
        Random r = new Random(); 
        System.out.println(r.nextInt(10));
    } 
}
```

`You might think that including so many classes slows down your program execution, but it doesn’t. The compiler figures out what’s actually needed.`

### Redundancy in imports

1 - **Every new Java program already have java lang imported by default**

2 - **Java follows order from top to bottom on imports**

3 - **Classes in the same package doesn't have to be imported**

### Wildcards

Wildcards only match classes names, not packages included

```java
//import java.nio.file.Files;
//import java.nio.file.Paths;

import java.nio.*; // WRONG
import java.nio.*.*; // WRONG - Only one wildcard allowed
import java.nio.file.Paths.* // WRONG - cannot import methods or attributes - Just classes
```

### Naming conflits
Java doesn't allow to import two classes from different packages with the same name (**Compilation error**) using wildcards. 

```java
//Both have Date classes
import java.util.*;
import java.sql.*;

public class Ex(){
    public static void main(String... args){
        Date date = new Date(); // COMPILATION ERROR
    }
}
```

Two things can be done to solve this problem

1 - Explicit import (no wildcard) will take precedence.

```java
import java.util.Date;
import java.sql.*;

public class Ex(){
    public static void main(String... args){
        Date date = new Date(); // Date from util
    }
}
```

2 - If needed to really use two classes with same from different packages than we need to declare a fully qualified class name

```java
import java.util.Date;

public class Ex(){
    public static void main(String... args){
        Date date = new Date(); // Date from util
        java.sql.Date sqlDate; 

        //or

        java.util.Date date;
        java.sql.Date date2;
    }
}
```

## Compiling and running code with packages

```bash 
javac packagea/ClassA.java packageb/ClassB.java
#or
javac packagea/*.java packageb/*.java

# Attention: Wildcard don't include subdirectories. Ex: packagea/subpacka/Class.java would not be compiled
```

## Using an Alternate Directory

