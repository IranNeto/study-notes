# Java Basics

## HashCode

Hash code is a value that identifies an object at runtime. When a given instance object calls `.hashCode()` the result
will always be the same. HashCode is used by Hash methods to identify objects at runtime. Ex: HashMap, HashSet, etc.

`equals()` and `hashCode()` have a contract between then.

1. For hash implementations
    1. Find the right bucket (using `.hashCode()`)
    2. Search the bucket for the right element (using `.equals()` )
2. Two objects being equals by `equals()` mean that its two contents are the same even if their references are not
   pointing to the same space in memory. But this doesn't mean the two object have the same _hashCode_
3. Two objects that have the same _hashCode_ doesn't mean that they are equals by `.equals()`. _hashCode_ collision can
   happen by chance or by human error.

```java
class Hash {
    public static void main(String[] args) {
        String a = "200";
        String b = "200";

        if (a.equals(b)) {
            System.out.println("Equal variables:");
            System.out.println(a.hashCode() + "\n" + b.hashCode());
        }

        String c = "10";
        String d = "50";

        if (!c.equals(d)) {
            System.out.println("\nUn-equal variables:");
            System.out.println(c.hashCode() + "\n" + d.hashCode());
        }
    }
}
```

### When someone should override equals and hashCode? How do they work?

When the object will be used as a key of any Hash implementations like HashMap, HashTable, HashSet, etc.
Continue with proof example in Hash implementations

### hashCode collision
