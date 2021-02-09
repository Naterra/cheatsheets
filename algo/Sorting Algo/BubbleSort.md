# Bubble Sort  

> Bubble sort is an algorithm that compares the adjacent elements and swaps their positions
if they are not in the intended order.
The process is repeated until all the elements are in their right position.The order can be ascending or descending.

**Ascending Order**: if first element is greater than the second,  swap elements. In this fashion, the largest value "bubbles" to the top.


 
![image](https://user-images.githubusercontent.com/8204364/107311928-537aed80-6a5d-11eb-95d3-1d7f66c0cd7f.png)

|       |Time                    | Space |
|-------|------------------------|-------|
| Best  | O(n) Linear (if the input array is already sorted) |O(1) |
| Avg.  | O(n²) Quadratic        |O(1)|
| Worst | O(n²) Quadratic        |O(1)|

**Space Complexity**: O(1) - because only a single additional memory space is required i.e. for tmp variable.



### Steps:
- Iterate through array of elements
- Compare current and next elements, if current is greater - swap them
- Repeat iterations until no swaps are needed.

### Overview:
Iteration 1: [**5**,3,1,4,6] → [3,**5**,1,4,6] → [3,1,**5**,4,6] → [3,1,4,**5**,6] → [3,1,4,**5**,6]   
Iteration 2: [**3**,1,4,5,6] → [1,**3**,4,5,6] → [1,3,4,5,6] → [1,3,4,5,6] → [1,3,4,5,6]   
Iteration 3: [1,3,4,5,6] → [1,3,4,5,6] → [1,3,4,5,6] → [1,3,4,5,6] → [1,3,4,5,6]   

As you can see, after iteration 2 the array is already sorted. 
Bubble sort, however, needs a final pass through the array to ensure that no 
other swaps are necessary before returning the array.

## Example #1
With this implementation, the code will run until the “i” variable is equal to the “len” variable, 
which means that it may run on an already sorted array more than once.
```javascript
//Time  O(n^2) - Quadratic Time

let bubbleSort = (inputArr) => {
    let len = inputArr.length;
    for (let i = 0; i < len; i++) {
        for (let j = 0; j < len; j++) {
            if (inputArr[j] > inputArr[j + 1]) {
                let tmp = inputArr[j];
                inputArr[j] = inputArr[j + 1];
                inputArr[j + 1] = tmp;
            }
        }
    }
    return inputArr;
};
```

## Example #2
Another slightly more efficient way to code bubble sort - is to keep track of a variable “swapped” which is initially set to
false. During each iteration, if values are swapped, then the “swapped” variable
is set to true. Then, using a do-while loop, it will only run the code if the
swapped variable is true, thus ensuring that only 1 extra verification iteration
happens.
```javascript
//O(n)??? - not sure
let bubbleSort = (inputArr) => {
    let len = inputArr.length;
    let swapped;
    
    do {
        swapped = false;
        for (let i = 0; i < len; i++) {
            if (inputArr[i] > inputArr[i + 1]) {
                let tmp = inputArr[i];
                inputArr[i] = inputArr[i + 1];
                inputArr[i + 1] = tmp;
                swapped = true;
            }
        }
    } while (swapped);
    return inputArr;
};
```

 
