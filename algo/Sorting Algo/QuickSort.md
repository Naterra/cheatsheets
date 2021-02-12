# Quick Sort  

> Quicksort uses the **divide-and-conquer strategy** to sort the given list of elements. This means that the algorithm breaks down the problem into subproblems until they become simple enough to solve directly.

Algorithmically this can be implemented either **recursively** or **iteratively**. However, the recursive approach is more natural for this problem

### Complexity

|       |Best           | Avg        |  Worst |
|-------|---------------|------------|--------|
| Time  |  O(n log n)   | O(n log n) | O(n²)  |
| Space |  x            | x          | x      |

**Logarithmic-time algorithm** up to 2x or even 3x faster than Merge Sort or Heap Sort. O(log n) speed is a best-case/average time, in worst case scenarios it can be O(n^2) depending on the implementation. 

### Characteristics
- **Divide-and-conquer** strategy
- **Unstable** sorting algorithm  

### Flow
1. Select an element of the array. This element is generally called the **pivot**. Most often this element is either the first or the last element in the array.   
2. Then, rearrange the elements of the array so that all the elements to the left of the pivot are smaller than the pivot and all the elements to the right are greater than the pivot. The step is called **partitioning**. If an element is equal to the pivot, it doesn't matter on which side it goes.   
3. Repeat this process individually for the left and right side of the pivot, until the array is sorted.
---

Let's understand these steps further by walking through an example. Consider an array of unsorted elements `[7, -2, 4, 1, 6, 5, 0, -4, 2]`. We'll choose the last element to be the pivot. The step-by-step breakdown of the array would be as shown in the image below:


<img width='500px' src='https://user-images.githubusercontent.com/8204364/107430311-f893d580-6af2-11eb-9c17-6725af7f7f15.png'/>

Elements that have been chosen as a pivot in one step of the algorithm have a colored outline. After partitioning, pivot elements are always in their correct positions in the array.

Arrays that have a bolded black outline represent the end of that specific recursive branch since we ended up with an array that contained only one element.

We can see the resulting sorting of this algorithm by simply going through the lowest element in each "column".




## Partition Implementation   

---

> There are many approaches to calculating the pivot value. While, some algorithms select the first item as a pivot, that’s not the best selection because it gives worst-case performance on already sorted arrays.


As we could see, the backbone of this algorithm is the partitioning step. This step is the same regardless of whether we use the recursive or iterative approach.
With that in mind, let's first write the code to partition() an array

#### Here is a logic behind it:   

---

<img width='900px' src='https://user-images.githubusercontent.com/8204364/107719876-36d1f600-6ca7-11eb-8849-ba82e773d1aa.png'/>

---
 
```javascript
const partition = (arr, start = 0, end = arr.length + 1) => {
    const swap = (list, a, b) => [list[a], list[b]] = [list[b], list[a]];

    let pivot = arr[start]; //at idx 0
    let pointer = start;    //at idx 0
    
    //loop array, if curr < pivot, swap curr with  pointer, then pointer++ 
    for (let i = start; i < arr.length; i++) {
        if (arr[i] < pivot) {
            pointer++;
            swap(arr, pointer, i);
        }
    };
    
    swap(arr, start, pointer); //swap pointer and pivot
    return pointer;
}
```
Here, we are taking the last element as the pivot. We are using a variable pointer (pivotIndex) to keep track of the "middle" position where all the elements to the left are less, and all the elements to the right are more than the pivotValue.

As the last step, we swap the pivot, which is the last element in our case, with the pivotIndex. So, in the end, our pivot element would end up in the "middle." With all elements less than the pivot to the left side of it, and all elements greater than or equal to the pivot to the right of the pivot.

 






## Iterative Solution
```javascript
function quickSortIterative(arr) {
    // Creating an array that we'll use as a stack
    stack = [0, arr.length - 1];

    // The loop repeats as long as we have unsorted subarrays
    while(stack.length > 0){
        // Extracting the top unsorted subarray
        end = stack.pop();
        start = stack.pop();

        pivotIndex = partition(arr, start, end);

        // If there are unsorted elements to the "left" of the pivot,
        // we add that subarray to the stack so we can sort it later
        if (pivotIndex - 1 > start){
            stack.push(start);
            stack.push(pivotIndex - 1);
        }

        // If there are unsorted elements to the "right" of the pivot,
        // we add that subarray to the stack so we can sort it later
        if (pivotIndex + 1 < end){
            stack.push(pivotIndex + 1);
            stack.push(end);
        }
    }
    return arr;
}
```


## Recursive Implementation
Now that we have the partition() function, we have to recursively break this problem down and apply the partitioning logic in order to do the remaining steps:

```javascript
function quickSortRecursive(arr, start=0, end=arr.length-1) {
    // Base case or terminating case
    if (start >= end) return;

    // Returns pivotIndex
    let index = partition(arr, start, end);

    // Recursively apply the same logic to the left and right subarrays
    quickSortRecursive(arr, start, index - 1);
    quickSortRecursive(arr, index + 1, end);
    return arr;
}
```

```javascript
//digitalOcean example
const sort = arr => {
  if (arr.length < 2) return arr;

  let pivot = arr[0];
  let left = [];
  let right = [];

  for (let i = 1, total = arr.length; i < total; i++) {
    if (arr[i] < pivot) left.push(arr[i]);
    else right.push(arr[i]);
  };
  return [
    ...sort(left),
    pivot,
    ...sort(right)
  ];
};
```


# References
- <a target='_bllank' href='https://stackabuse.com/quicksort-in-javascript/'>Quick Sort</a>
 


