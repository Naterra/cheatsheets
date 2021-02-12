# Group consecutive numbers in ranges


Given a series of integers, group consecutive numbers in ranges, as such:
```javascript
Sample input: (2,3,4,5,9,8,10,13)
Sample output: ( (2,5), (8,10), (13, 13)  )

i: (4,2,3)
o: ((2,4))

i: [2, -1, 1, 0, -5, -7, -6]
o: [[-7,-5], [-1, 2] ]
```

There is no duplication and the list is not sorted

## Solution
> Solution: Two Pointers Technique  
> Time Complexity: O(N), where N is the length of the array


```javascript
function formattedArr(arr) {
    const res=[];

    arr = arr.sort((a,b)=>(a-b)); //sort array

    let start=null; //pointer

    for(let i=0; i< arr.length; i++){
        let curr=arr[i];
        let next=arr[i+1];
        if(!start) start = curr; //define initial number of range
        
        //if next != current value +1, then sequence is broken
        if(next != curr+1){
            res.push([start, curr]);
            start=null;
        }
    }

    return res;
};

const arr = [2, -1, 1, 0, -5, -7, -6];
const newArr = formattedArr(arr); //[[-7,-5], [-1, 2] ]
```
<mark>!</mark> Be careful with **for in** loop, its index typeof is a string.  

### ES6
The iteration over array elements could be implemented using .entries() method.
In this case we would have access to index (number) and its value without any extra steps.
- destructuring syntax
```javascript
 for(let [i, curr] of arr.entries()){
    ...
  }
```

