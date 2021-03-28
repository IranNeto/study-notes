# Interface Segregation Principle - ISP

`stability` / `spread of change` / `polymorfism`

Clients should not be forced to depend upon interfaces that they do not use or unstable interfaces. Any interface changes, cause less impact on the class which implements it.
ISP is another principle to decrease the spread of changes.

**What is a Class/Interface stable?**

A sign of stability in interfaces is that one which has many implementations, for example, the List interface has some implementations, such as ArrayList, 
LinkedList or SkipList. 

**But, why this is a sign of stability?**

Having multiple implementations decreases the chances of crashing caused by a change in the interface, once a change is done,
it could affect all its implementation, then it's risky to change this interface without cause side effects. With this in mind, interfaces, such as List, are more reliable.

```
└── List
    ├── ArrayList
    └── LinkedList
    └── SkipList
```

**Implement an interface isn't couple a class to its interface contract?**

Yes. In general, the coupling is bad, BUT, *it's is impossible to reduce coupling to 0*.

There are 2 types of coupling: **Afferent coupling** and **Efferent coupling**

Afferent coupling

* **Who depends on you**.
* Measure how many other packages use a specific package.
* Incoming dependencies.

Efferent coupling

* **Who do you depend on**.
* Measure of how many different packages are used by a specific package.
* Outgoing dependencies.

**Why are these types of coupling important?**

Remember what we've already told about class/interface stable. So, let's look at the mathematical definition of stability with packages.

Instability (I): The ratio of efferent coupling (Ce) to total coupling (Ce + Ca) such that I = Ce / (Ce + Ca). This metric is an indicator of the package's resilience to change. 
The range for this metric is 0 to 1, with I=0 indicating a completely stable package and I=1 indicating a completely unstable package.

In short, decreasing Ce and increasing Ca, is the way to reach package stability. 
`That means, reducing classes which you depend on and increasing classes which depends on you.` As we said in the beginning.

Coupling must show who is stable or not.

`Program looking to stable interfaces`