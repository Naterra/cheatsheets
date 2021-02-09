# Insertion Sort

Insertion sort works by moving from left to right over an input list. You could compare it to the way you would sort a set of cards that you were holding in your hand. You’d scan the set from left to right, grabbing each card as you go and moving it to the position where the card to it’s left would be smaller or equal to the current card’s value. After you move the card furthest to the right, you’ll be left with a set of cards that has been sorted in ascending order. Insertion sort will use the current item as a “key”, and then search through the items to the left of that item in the input list for the place that the key should go. This means that the sub-list to the left of the current “key” will already be sorted, and will remain sorted after every iteration of insertion sort.

### Complexity
|       |Time                    | Space |
|-------|------------------------|-------|
| Best  | O(n) Linear (if the input array is already sorted) |O(1) |
| Avg.  | O(n²) Quadratic        |O(1)   |
| Worst | O(n²) Quadratic        |O(1)   |

**Space**: Because insertion sort sorts your list in-place, it only uses O(1) (constant) space.


<img width='400' src='https://user-images.githubusercontent.com/8204364/107319662-4108b000-6a6d-11eb-88aa-789c2d45a855.png'/>


### Benefits
- **Efficient for small data sets**, but very inefficient for larger lists.   
- **Adaptive**, that means it reduces its total number of steps if a partially
  sorted array is provided, making it efficient. It reduces it’s run time to O(nk) where each
  element in the list is no more than k elements away from it’s sorted position.   
- Usually **more efficient than other quadratic sorting algorithms** (**Bubble Sort** or **Selection Sort**)     
- **Outperforms** quick sort or merge sort on lists of 10-20 elements. 
- Its space complexity is less. Like Bubble Sort, insertion sort also requires a single additional memory space.   
- It is a **stable sorting algorithm**, as it does not change the relative order of elements which are equal.   



 
### Steps:
Iteration 0: [5,3,1,4,6]  
Iteration 1, key is 3 (at index 1): [5,**3**,1,4,6] →[3,5,1,4,6]  
Iteration 2, key is 1 (at index 2): [3,5,**1**,4,6] →[1,3,5,4,6]  
Iteration 3, key is 4 (at index 3, ): [1,3,5,**4**,6] → [1,3,4,5,6]  
Iteration 4, key is 6 (at index 4): [1,3,4,5,**6**] → [1,3,4,5,6] — because 6 was already in the right place, no changes are made and insertion sort returns the sorted array. Notice how after each step, all the items to the left of the key are already sorted.

```javascript
let insertionSort = (inputArr) => {
    for (let i = 1; i < inputArr.length; i++) {
        let key = inputArr[i];
        let j  = i - 1;
        while (j >= 0 && inputArr[j] > key) {
            inputArr[j + 1] = inputArr[j];
            j--;
        }
        inputArr[j + 1] = key;
    }
    return inputArr;
};
```

### Resources
https://medium.com/javascript-algorithms/javascript-algorithms-insertion-sort-59b6b655373c
