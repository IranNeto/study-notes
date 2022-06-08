# Java core

* String Pool
    * What's the String Pool and how does it work?
* Immutability vs Mutability
* Concatenation
    * How concatanation works in Java?
    * Why using + operator for Strings can be harmfull?
* Equality
    * How does it work String equality with == vs .equals()?
* String API


## String

String is a special class in which it doesn't need to be instantiated with `new`. String implements `CharSequence` interface that which is a general way of representing several classes involving String - such as String itself and StringBuilder.

How does Java stores a string value without new? R: **String Pool**
String is pretty common in lots of Java application and they can consume a lot of memory. To improve perfomance, Java try to reuse common Strings used by the application by storing them in the String Pool.

**String Pool == Internal Pool, is a location in the memory where JVM collect these strings.**


```java
String a = "Java";
String b = "Java";
String c = new("Java");

System.out.println(a == b); //true
System.out.println(b == c); //true
```

Strings are immutable and literals are pooled. The JVM pools just String a. String b and c just have the same reference as String a. So in this way, JVM saves 2 String references by making all of them using the same one.


## Equality

## Concatenation

Concatenation is the operation of putting an object in front of the other. Using the `+` operator can be used in two ways within the same line of code.

```java
System.out.println(1 + 2); //Both operands are numeric means numeric addition -> 3
System.out.println("a" + "b"); //Both operands are Strings means String concatenation -> ab
System.out.println("a" + "b" + 3); //Since we start from left to right, here means a string as result -> ab3
System.out.println(1 + 2 + "c"); //Starting from left to right, the first operation is a numeric one. But there's a third string operand -> 3c
System.out.println("c" + 1 + 2); //Start with a String then everything else will be treated as string: c1 and after c12 -> c12

int three = 3;
String four = "4"; 
System.out.println(1 + 2 + three + four); //64 (String)

String s = "1";        //s holds "1"
s += "2";              //s holds "12"
s += 3;                //s holds "123"
System.out.println(s); //"123"
```
## Immutalibility

Strings once created are placed in perfect size memory "boxes" where it's not possible to:
* strech or shrink to fit any string change.
* change any character inside it.

**This is called immutability.**

```java
String s1 = "1";
String s2 = s1.concat("2");
s2.concat("3");
System.out.println(s2); //12

/*
Strings are immutable class so s2.concat("3") returns a new string without modify s2
*/
```
the `final` keyword concept is related to immutability. To make a custom variable or class immutable you can just add `final` to its declaration to avoid subclasses creation/modification. 

> You don't want to have a mutable behavior in something that should be immutable


## String API

### .lenght()
The method `int length()` returns the number of characters in the String.

### .charAt()
The method `char charAt(int index)` returns the char at a certain index.

OBS: Any invalid index throws an IndexOutOfBoundsException

### .indexOf()

The method indexOf() looks at the characters in the string and finds
the first index that matches the desired value.

    int indexOf(int ch)
    int indexOf(int ch, int fromIndex)
    int indexOf(String str)
    int indexOf(String str, int fromIndex)
    
### .substring()
The method substring() returns a piece of a string defined by the indexes

    String substring(int beginIndex)
    String substring(int beginIndex, int endIndex)
    
If the beginIndex is bigger then the endIndex or endIndex goes beyond the lenght 
an exception is generated.

### .toLowerCase() and .toUpperCase()

toLowerCase() and toUpperCase() is respectively all caps or none caps

