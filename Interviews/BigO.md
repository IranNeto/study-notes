# Big O

Big O time is the metric we use to describe the effiency of algorithms.

Big O means time complexity with the concept of asymptotic runtime. How much the
time to run an algorithm grows variaying a certain parameter.

`O(1), O(n), O(n log(n)), O(xˆn), O(log(n)), O(nˆx), O(n!)`

## Big O, Big Theta, Big Omega

1. **Big O** describe an upper bound on the time. The maximum time complexity an algorithm can reach.

2. **Big Omega** describe the lower bound. An algorithm cannot be faster or less complex than this.

3. **Big Theta** means both Big O and Big Omega. When an algorithm has the same complexity for O and Omega then Theta.

## Best, Worst, and Expected cases

Giving a scenario of a sort algorithm

1. **Best case** scenario happens when the input array is already sorted

2. **Worst case** scenario happens when the input array is reversed sorted

3. **Expected case** scenario usually means the possibilities between the best and worst cases. What are the expected.

> Best, worst, and expected cases describe the big O (or big theta) 
> time for particular inputs or scenarios.
> Big 0, big omega, and big theta describe the upper, lower, and 
> tight bounds for the runtime.

## Space complexity

Space complexity is a parallel concept to time complexity. Filling an array of
size N means that it would take O(N) space, a two dimensional array would take
O(Nˆ2) space and so on.

> Stack space in recursive calls counts too. For example, N 
> recursive calls would take O(N) space and time complexity.

## Amortized Time

Some operations can cost way higher once in a while. For example, 
`ArrayList` is an dynamic resizing array implementation that double
the capacity every time the capacity is reached. So if we want to insert an element
in a already full array it will double the size and copy all the elements to the new 
array. Let's consider an ArrayList of size N, therefore the insertion operation is 
O(N). But this happens rarely, in normal conditions we have O(1) time for insertion.

Taking everything for account means that insertion take O(2N) time. The amortized 
time for each insertion is O(1).

> Considering an ArrayList size N, it must had be initiated with size 1. Until reach
> N it should doubled the size until N. So the sizes with time were 1, 2, 4, 8, 16, ... N.
> Reading right to left we have N + N\2 + N\4 + ... + 1 = 2N

## Recursive runtimes

```java
int f(int n){
    if(n <= 1) return 1;
    return f(n - 1) + f(n - 1);
}
```

Each time we call the function f we're making to more calls. This builds an binary
tree of calls. The tree will have depth N. The number of nodes in each level is 
2^Ndepth. The total nodes will be 2ˆ(N+1) - 1.

The space complexity will be O(N) since would be N calls to the function maximum
at the same time. For time complexity we'd have usually O(branches^depth). In this case O(2ˆN).