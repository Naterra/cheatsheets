# Runtime Complexity

> Describes the performance of an algorithm  
> Runtime Complexity - is a reference to performance of an algorithm  

> Space Complexity - is a reference to how much ram or memory or space an algorithm needs to complete a given task.

>Space Complexity and Time Complexity are not always would be identical.


- O(1) - Constant Time
- O(log N) - Logarithmic Time
- O(N) - Linear Time  
- O(n log n) - Quasilinear Time
- O(n^2) - Quadratic Time
- O(2^n) - Exponential Time 
- O(n!) - Factorial Time 
 
<img width='400' src='https://miro.medium.com/max/2928/1*5ZLci3SuR0zM_QlZOADv8Q.jpeg'/>


| Problem   | Time Complexity        |
|-----------|------------------------|
| Iterating with a simple  for loop through a single collection  | O(n)|
| Iterating through half  a collection? | Still O(n)|
| Iterating through 2 different collections with separate for loops?| O(n + m)|
| Two nested for loops iterating over the same collection?| O(n^2) |
| Two nested for loops iterating over different collections?| O(n*m) |
|Sorting?     | O(n*log(n))|
|Searching through sorted array? | O(log(n))|


## O(1) - Constant Time
An algorithm is said to be constant time (also written as O(1) time) if the value of T(n) is bounded by a value that does not depend on the size of the input. For example, accessing any single element in an array takes constant time as only one operation has to be performed to locate it.

```javascript
//Example 1:
const getItem = (idx, arr) => arr[idx];
getItem(idx, [1,2,3]);
getItem(idx, [1,2,3,4,5,6,7,8,...]); //still one step to access value

//Example 2:
function isEvenOrOdd(n) {
    return n % 2 ? 'Odd' : 'Even';
}
```



## O(log N) - Logarithmic
An algorithm is said to have a logarithmic time complexity when it reduces the size of the input data in each step (it don’t need to look at all values of the input data)

The best analogy I’ve heard to understand logarithmic growth is to imagine looking up a word like 'notation’ in a dictionary. You can’t search one entry after the other, instead you find the 'N’ section, then maybe the 'OPQ’ page, then search down the list alphabetically until you find a match.

With this 'divide-and-conquer’ approach, the amount of time to find something will still change depending on the size of the dictionary but at nowhere near the rate of O(n). Because it searches in progressively more specific sections without looking at most of the data, a search through a thousand items may take less than 10 operations while a million may take less than 20, getting you the most bang for your buck

- Binary Search
- Dictionary search
- Quick Sort

[comment]: <> (- Searching through array of data)

```javascript
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


## O(N) - Linear Time
An algorithm is said to have a linear time complexity when the running time increases at most linearly with the size of the input data. This is the best possible time complexity when the algorithm must examine all values in the input data.

Example: Loop through the list of elements.  
O(N) - N is the length of the array.

- Linear Search

```javascript
function printArray(arr){
    for(let i of array){
        console.log(i);
    }
}
 
printArray([1,2,3,4,5]); //5 elements
printArray([1,2,3,4,5,6,7,8,9,.....]); //n elements
```


## O(n log n) - Quasilinear Time
An algorithm is said to have a quasilinear time complexity when each operation in the input data have a logarithm time complexity. It is commonly seen in sorting algorithms (e.g. mergesort, timsort, heapsort).
- mergesort, 
- timsort, 
- heapsort

```javascript

```


## O(2N)
```javascript
function printArray(arr){
    //1st loop O(N)
    for(let i of array){ console.log(i); }
    
    //2nd loop  O(N)
    for(let i of array){ console.log(i); }
    
    // O(N) +  O(N) =  O(2N)
}
 
printArray([1,2,3,4,5]);
```

## O(N<sup>2</sup>) - Quadratic Time
An algorithm is said to have a quadratic time complexity when it needs to perform a linear time operation for each value in the input data.

- Bubble Sort

```javascript
function table(rows, cols){
    //1st loop O(N)
    for(let r of rows){
        ...
        for(let c of cols){
            ...
        } 
    }
}
//O(n * n) = O(N^2)
```



## O(2<sup>n</sup>) - Exponential Growth
An algorithm is said to have an exponential time complexity when the growth doubles with each addition to the input data set. This kind of time complexity is usually seen in brute-force algorithms.

- recursive calculation of Fibonacci numbers

```javascript

```


## O(n!) - Factorial
An algorithm is said to have a factorial time complexity when it grows in a factorial way based on the size of the input data.
As you may see it grows very fast, even for a small size input.

- Heap’s algorithm

> 2! = 2 x 1 = 2  
> 3! = 3 x 2 x 1 = 6  
> 4! = 4 x 3 x 2 x 1 = 24  
> 5! = 5 x 4 x 3 x 2 x 1 = 120  


## Important Notes
It is important to note that when analyzing the time complexity of an algorithm with several operations we need to describe the algorithm based on the largest complexity among all operations.

```javascript
function example(arr){
    const firstElement = arr[0]; // O(1) - Constant time
    
    for(let i of arr){  // O(n) - Linear time
        console.log(i);
    }

    for(let x of arr){  // O(n^2) - Quadratic time
        for(let y of arr){
            console.log(x+y);  
        }
    }
}

//O(1) + O(n) + O(n^2)
```
When increasing the size of the input data, the bottleneck of this algorithm will be the operation that takes O(n²).    

Based on this, we can describe the time complexity of this algorithm as O(n²).

## Big-O Cheat Sheet
<img width='400' src='https://miro.medium.com/max/1400/1*Uzrw9faXdYgg20I6NjUTBw.png'/>

Here is another sheet with the time complexity of the most common sorting algorithms.

<img width='400'  src='https://miro.medium.com/max/1400/1*X1hZCxNdfgZ0sT_2tynPKA.png'/>


# References
- <a target='_bllank' href='https://towardsdatascience.com/understanding-time-complexity-with-python-examples-2bda6e8158a7'>Understanding time complexity</a>
- <a target='_bllank' href='https://adrianmejia.com/most-popular-algorithms-time-complexity-every-programmer-should-know-free-online-tutorial-course'>8 time complexities that every programmer should know | Adrian Mejia Blog </a>
- <a target='_bllank' href='https://www.digitalocean.com/community/tutorials/js-big-o-notation'>Understanding Big O Notation via JavaScript-DigitalOcean</a>

https://adrianmejia.com/most-popular-algorithms-time-complexity-every-programmer-should-know-free-online-tutorial-course/
https://www.jenniferbland.com/time-complexity-analysis-in-javascript/
