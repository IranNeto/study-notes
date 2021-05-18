# Techniques

These are some techniques I observed while solving some probleming in leetcode

## Arrays

* Distinct elements

Distinct elements usually means that they can be mapped into a hashmap to be searched with O(1)

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

Example: https://leetcode.com/problems/game-of-life/

* Saving update states to be executed when needed

In this example https://leetcode.com/problems/subrectangle-queries/discuss/1187389/Java-faster-greater97.67-mem-less-97.17 we have a class with 2 operations: update matrix and get value.
The first idea is to update the matrix in the brute force way with 2 nested loops but there's also another strategy. It's possible to store all update infos and "apply" them when the get value operation is
required. That can be a good trade off depending on the number of update and get values we have.

brute force: update O(n**2) getValue O(1)
clever way: update O(1) getValue O(number of updates)