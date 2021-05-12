# Data Structure Summary

## Arrays

### Pros

* **Lookup** is great - random access, constant time O(1) - No need to cross
* Easy to sort
* Small size-wise

### Cons

* **Insertion** is bad - lots of shifting and lifting elements in the middle
* **Deletion** is bad - lots of shifting and lifting after removing an element
* Stuck with a fixed size, no flexibility

> Attention to the resizeble Arrays. They might double its size every time
> the array reach the limit. After that all the previous elements are copied to 
> the new array

## Linked List

### Pros

* **Insertion** is easy - just tack onto the front - last element just points to the new element
* **Deletion** is easy - once find the element - just change the next pointer to the element after the deleted one (or two if it is a doubled linked list)
* Relatively small size-wise (not as small as arrays)
* 
### Cons

* **Lookup** is bad - Have to rely on linear search - Cross all the list
* Hard to sort - unless you are willing to compromise on super-fast insertion and instead sort as you construct. Then insertion gets slower

## Hash tables

### Pros
* **Insertion** is a two-step process - hash then add.
* **Deletion** is easy - once you find the element. Probing vs chaining
* **Lookup** is on avarage better than with linked lists because you have the benefit of a real-world contant factor.

### Cons
* Not an ideal data structure if sorting is the goal - just use an array
* Can run the gamut of size

## Trie

### Pros
* **Deletion** is easy - just free a node
* **Lookup** is fast - not quite as fast as an array, but almost
* Already sorted - sorts as you build in almost all situations
  
### Cons  
* **Insertion** is complex - a lot of dynamix memorix allocation, but gets easier as you go
* Rapidly becomes huge, even with very little data present, not great if space is at a premium.