# Java Basics

## HashCode

Hash code is an value that identifies an object at runtime. When a given instance object calls `.hashCode()` the result will always be the same.
`equals()` and `hashCode()` have similarities beetween then. If two objects are equals by `equals()` it means the two references are pointing to the same
space in memory. Therefore they are equal and have the same hash code.

```java
class Hash{
    public static void main(String[] args){
        String a = "200";
        String b = "200";

        if(a.equals(b)){
            System.out.println("Equal variables:");
            System.out.println(a.hashCode() + "\n" + b.hashCode());
        }

        String c = "10";
        String d = "50";

        if(!c.equals(d)){
            System.out.println("\nUn-equal variables:");
            System.out.println(c.hashCode() + "\n" + d.hashCode());
        }
    }
}
```
