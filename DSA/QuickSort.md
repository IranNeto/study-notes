# Quick Sort

Quick Sort is an algorithm well-known for sorting an array.
It's strategy is based on divide and conquer one. It will pivot an element and divide two sections of this element to be sorted recursivelly.

The first part of the algorithm then is choosing and placing the pivot element. While placing the pivot, some swaps are made in order to reach a state
where all elements at pivot's left are smaller than it, and by definition all elements at right are greater than it.

With this array state, the Array left and Array right are recursively pivoted and swapped until everything is sorted.

### Pseudocode 

This approach chooses the last element as inital pivot but some variation can be adapted 

1. First element as pivot
2. Random element as pivot
3. Median element as pivot
   
```
algorithm quicksort(A, lo, hi) is
    if lo < hi then
        p := partition(A, lo, hi)
        quicksort(A, lo, p - 1)
        quicksort(A, p + 1, hi)

algorithm partition(A, lo, hi) is
    pivot := A[hi]
    i := lo
    for j := lo to hi do
        if A[j] < pivot then
            swap A[i] with A[j]
            i := i + 1
    swap A[i] with A[hi]
    return i
```

The implementation in Java is

```java
public class QuickSort {

    public static int partition(int[] arr, int lo, int hi){
        //i is an indicator of where the pivot should be after all
        int pivot = arr[hi];
        int i = lo;
        for(int j = lo; j < hi; j++){
            if(arr[j] < pivot){
                int temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
                i += 1;
            }
        }
        int temp = arr[i];
        arr[i] = arr[hi];
        arr[hi] = temp;
        return i;
    }

    public static void quicksort(int[] arr, int lo, int hi){
        if(lo < hi){
            int p = partition(arr, lo, hi);
            quicksort(arr, lo, p - 1);
            quicksort(arr, p + 1, hi);
        }
    }

    public static void main(String[] args) {
        var arr = new int[]{30, 80, 90, 5, 10, 100, 70};
        quicksort(arr, 0, arr.length - 1);
        System.out.println(Arrays.toString(arr)); //[5, 10, 30, 70, 80, 90, 100]
    }
}
```

## Complexity

The time analysis can be written as 

```
T(n) = T(k) + T(n - k - 1) + Theta(n)

T(k) + T(n - k - 1) are factor for the recursive calls

n = array's size
k = number of elements smaller than the pivot 
```

### Worst case

The worst case happens when the pivot is the smallest or the greatest element in the array. For example, considering the variation of
choosing the last element of the array, then the worst case would be a already sorted array ascended or descended ordered.

In this case the time analysis can be written as

```
T(n) = T(0) + T(n - 1) + Theta(n)
T(n) = T(n - 1) + Theta(n)
T(n) = Theta(nˆ2)
n = array's size
```

### Best case

The best case occurs then when the middle element is picked as pivot. In this case

```
T(n) = T(n/2) + T(n/2) + Theta(n)
T(n) = 2T(n/2) + Theta(n)
T(n) = Theta(n*logn)

n = array's size
```

### Average case

The average case can be defined by all possible array permutation and take every time. Instead of this we're supposing an case. Let's say that
the partition puts O(n/10) elements in one set and O(9n/10) elements in other set. In this case we have

```
T(n) = T(n/10) + T(9n/10) + Theta(n)
T(n) = Theta(n*logn)

n = array's size
```

## Conclusion 
 
> Although the worst case time complexity of QuickSort is O(nˆ2) which is more than many other sorting algorithms like Merge Sort and Heap Sort, QuickSort is faster 
> in practice, because its inner loop can be efficiently implemented on most architectures, and in most real-world data. QuickSort can be implemented in different 
> ways by changing the choice of pivot, so that the worst case rarely occurs for a given type of data. However, merge sort is generally considered better when data 
> is huge and stored in external storage. (Geeks for geeks)

Is QuickSort **stable**? 
The default implementation is not stable. However any sorting algorithm can be made stable by considering indexes as comparison parameter. 

Is QuickSort **In-place**? 
As per the broad definition of in-place algorithm it qualifies as an in-place sorting algorithm as it uses extra space only for storing recursive function calls but not for manipulating the input. 

More information: https://www.geeksforgeeks.org/quick-sort/
