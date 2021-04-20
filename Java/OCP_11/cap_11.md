# Modules

The Java Platform Module System (JPMS) was introduced in Java 9 to group code at a higher level
and tries to solve the problems that Java has been plagued with since the beginning: Jar hell.

Module is to provide groups of related packages to offer a
particular set of functionality to developers. It’s like a JAR file except a developer chooses
which packages are accessible outside the module.

The Java Platform Module System (JPMS) includes the following: 
* A format for module JAR files
* Partitioning of the JDK into modules
* Additional command-line options for Java tools

A module is a group of one or more packages plus a special file called **module-info.java**.

## Benefits of modules (IMPORTANT)

### Better access control
The traditional access modifiers (public, default, protected and private) allow controling
the access to certain class or packages. But inside a module, there is no way of allowing 
access to a certain class just to an specific module and not others. That is where modules
come. It is possible to module-info.java

### Clear Dependency management
Some libraries depend on other libraries to work properly. If some dependecy is not on
classpath, a error is generated when the missing library is needed at run time. With modular control
it is possible to know right away if a mandatory dependency is missing.

### Custom Java Builds
The full JDK is pretty big (150MB) and despite the fact that some attempts were made in the past
to give more flexibility to the build. None of them were very successful.

The Java Platform Module System allows developers to specify what modules they actually need.
This makes it possible to create a smaller runtime image that is customized to what the application
needs and nothing more. **Users can run that image without having Java installed at all**.

A tool called jlink is used to create this runtime image.

### Improved Performance
Since Java now knows which modules are required, it only needs to look at those at class
loading time. This improves startup time for big programs and requires less memory to run.

### Unique Package
Another manifestation of JAR hell is when the same package is in two JARs. There are a number
of causes of this problem including renaming JARs, clever developers using a package name that
is already taken, and having two versions of the same JAR on the classpath.
The Java Platform Module System prevents this scenario. A package is only allowed to be supplied by one module.

## Creating the files

```java
//Task.java
package zoo.animal.feeding;

public class Task {
    public static void main(String... args) {
        System.out.println("All fed!"); 
    }
}
```

```java
//module-info.java
module zoo.animal.feeding{}
```

### Differences between module-info and java class

* The module-info file must be in the root directory of your module. Regular Java classes should be in packages.

* The module name follows the naming rules for package names. It often includes periods (.) in its name.
**Regular class and package names are not allowed to have dashes (-). Module names follow the same rule**.

* The module-info file must use the _keyword_ module instead of class, interface, or enum.

It is possible to have a module-info.java empty.

## Compiling the module

```shell script
javac --module-path mods -d feeding feeding/zoo/animal/feeding/*.java feeding/module-info.java
```

* `-d` indicates the directory to put the class files
* `--module-path` or `-p` indicates the location of any custom module file that we are depending on?
*  The last two arguments are java files to be compiled

module-path replaces the classpath option

-cp, -class-path, -classpath is still used in nonmodular programs

## Run the module

