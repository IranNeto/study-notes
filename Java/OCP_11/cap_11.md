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

* `--module-path` or `-p` indicates the location of any custom module file that we are depending on?
* `-d` indicates the directory to put the class files
*  The last two arguments are java files to be compiled

module-path replaces the classpath option

-cp, -class-path, -classpath is still used in nonmodular programs

## Run the module

```shell script
java --module-path mods -- module/com.sybex.OCP
```

* `--module-path` indicates `mods` as the location of modules
* `--module <module name>` points to existing module's name `book.module`
* It is important to have the slack to **sepatate module/package**
* `com.sybex` is the package name
* `OCP` is the class name

## Packaging a module

```shell script
java -cvf mods/zoo.animal.feeding.jar -C feeding/ .
```
## Diving into the module-info File

`exports` and `requires` are keywords inside a module-info.java

**exports** exports a package to other modules. It's also possible to export a package to a specific module.
With module-info.java below, ONLY staff module is able to import zoo.talks.content.

```java
module zoo.anumal.talks {
    exports zoo.animal.talks.content to zoo.anumal.staff;
    exports zoo.animal.talks.media;
    requires zoo.animal.feeding;
    requires zoo.animal.care;
}
```
Access control with modules

| Level |   Within module code    | Outside module  |
|-------|-------------------------|-----------------|
| private | Available only within class | No access |
| default | Available only within package | No access |
| protected | Available only within package or to subclasses | Accessible to subclasses only if package is exported |
| public | Available to all classes | Accessible to subclasses only if package is exported |

`requires moduleName` menas that the current module depends on the _moduleName_. But there's also a `requires transitive`
which means that any module that requires the current module will also depende on _moduleName_.

**Java doesn't allow to repeat the same module in a requires clause. It is redundant to require a module
and requires transitively the same module.

## Discovering modules

### Describing a Module. 

Describing an jar file structure

```shell script
java -p mods -d zoo.animal.feeding
java -p mods --describe-module zoo.animal.feeding 
```

_java.base_ is special in every module because it is automatically added as a dependency to all modules.

### Listing available modules

```shell script
java --list-modules

# All modules that come with java
java.base@11.0.2
java.compiler@11.0.2
java.datatrasnfer@11.0.2

java -p mods --list-modules

#Custom modules and its location
zoo.animal.care file:///absolutePath/mods/zoo.animal.care.jar 
zoo.animal.feeding file:///absolutePath/mods/zoo.animal.feeding.jar 
zoo.animal.talks file:///absolutePath/mods/zoo.animal.talks.jar 
zoo.staff file:///absolutePath/mods/zoo.staff.jar

java --show-module-resolution -p feeding -m zoo.animal.feeding/zoo.animal.feeding.Task

#Way to debug modules. It spits out when the program starts up then it runs the program

root zoo.animal.feeding file:///absolutePath/feeding/
java.base binds java.desktop jrt:/java.desktop
java.base binds jdk.jartool jrt:/jdk.jartool
...
jdk.security.auth requires java.naming jrt:/java.naming jdk.security.auth requires java.security.jgss jrt:/java.security.jgss ...
All fed!
```

### Using jar command


