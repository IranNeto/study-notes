# Techniques

These are some techniques I observed while solving some probleming in leetcode

## Arrays

* N pointers

Sometimes to find right position or an interval in arrays we can use pointers i, j (for example) and slide them across the array
`Slide` - `windowing`

* Sum array elements without sum variable

In some cases we're gonna need to sum the elements of an array and for that the intuitive way is to create a global sum variable and update it through the for loop.
But, instead of that check for the possibility of initiate the first position and then find the next position by the previous position.

Example: https://leetcode.com/problems/running-sum-of-1d-array/

* Creating new representional states

In some cases we're gonna need to represent states i.e 0 == dead, 1 == alive. But, it we may reach a problem when an in-place solution is required and the neighbors states are part of the problem. 
So we can expand and create new representional states i.e 2 == dead but before was alive, 3 == alive but before was dead

