# Selection Sort

>**Selection sort algorithm** is grounded on the logic of finding the minimum 
> element in an array and sort accordingly. The selection sort algorithm is actually
> an **in-place comparison based algorithm** in which the entire input array is divided
> into two sections, the sorted array on the left and the unsorted array on the right.

### Complexity
|       | Time                   | Space |
|-------|------------------------|-------|
| Best  | O(n²) Quadratic        | O(1)  |
| Avg.  | O(n²) Quadratic        | O(1)  |
| Worst | O(n²) Quadratic        | O(1)  |




### Characteristics
- In-place comparison based algorithm, Unstable   
- Better than Quicksort or Merge Sort (if the input collection is small).   
- Compared to other quadratic time complexity algorithms (Bubble Sort, Insertion), SS holds itself quite well, outperforming Bubble Sort and its variants, as well as Gnome Sort.
- Insertion sort can be faster than Selection Sort in case the collection is almost sorted. And Insertion Sort is pretty much unbeaten with short collections.
- The disadvantage of the selection sort is its poor efficiency when dealing with a huge list of items. 

### Flow
This algorithm divides the input array into two sublists - a sorted and unsorted sublist. The sorted list is located at the start of the collection, and all elements to the right of the final sorted element are considered unsorted.
Initially, the sorted list is empty, while the rest of the collection is unsorted. Selection Sort goes through the unsorted sublist and finds the smallest or largest element.
The element is then swapped with the leftmost element of the unsorted sublist. Then, the sorted sublist is expanded to include that element.


<img width='400px' src='https://user-images.githubusercontent.com/8204364/107403863-a1323d00-6ad3-11eb-960b-734ed0a48e3d.png'/>

<img height='150px' src='https://stackabuse.s3.amazonaws.com/media/selection-sort-in-javascript-1.gif'/>    

 
```javascript
function selectionSort(inputArr) { 
    for(let i = 0; i < inputArr.length; i++) {
        // Finding the smallest number in the subarray
        let min = i;
        // loop thourgh the array from the next element of the array. This will help us in checking 
        // only against the unsorted elements, as we know the elements before it are already sorted.
        for(let j = i+1; j < n; j++){
            if(inputArr[j] < inputArr[min]) {
                min=j; 
            }
         }
         if (min != i) {
             // Swapping the elements
             let tmp = inputArr[i]; 
             inputArr[i] = inputArr[min];
             inputArr[min] = tmp;      
        }
    }
    return inputArr;
}
```

### Selection Sort Variants
the most famous variant is Heap Sort, which internally uses a heap data structure for storing elements. Using heaps can speed up the finding and removal of elements to an O(logn) time.

This is a very beneficial optimization that reduces the total running time from O(n^2) to O(nlogn), which is considered good for sorting algorithms.

Another variant is the BidirectionaL Selection Sort, similar to how Bubble Sort has a bidirectional counterpart. It's sometimes known as Cocktail Sort (again, similar to Bubble's Cocktail Shaker Sort), and does the same job in ~25% fewer comparisons.
  
### Complexity Analysis
In Selection Sort, n-1 comparisons will be done in the 1st pass, n-2 in 2nd pass, n-3 in 3rd pass and so on.

So the total number of comparisons will be,  
(n-1) + (n-2) + (n-3) + ..... + 3 + 2 + 1  
Sum = n(n-1)/2 = ½ [ n2 – n]  
i.e. O(n2)  

Hence the time complexity of Selection Sort is O(n^2).   
Worst and Average case time complexity: O(n^2)
Best case time complexity: O(n) (i.e., when the list is already sorted)  

**Space complexity** is O(1) because only a single additional memory space is required for temp variable.




### Resources
- <a target='_blank' href='https://stackabuse.com/selection-sort-in-javascript/'>Selection Sorting / StackAbuse</a>
- <a target='_blank' href='https://www.faceprep.in/algorithms/selection-sort/'>Selection Sorting / FacePrep</a>

