# Array Chunk

Given an array and chunk size, divide the array into many subarrays where each subarray is of length size.

### Example

```javascript
chunk([1,2,3,4], 2) --> [[1,2], [3,4]]
chunk([1,2,3,4,5], 2) --> [[1,2], [3,4], [5]]
chunk([1,2,3,4,5,6,7,8], 3) --> [[1,2,3], [4,5,6], [7,8,9]]
chunk([1,2,3,4,5], 10) --> [[1,2,3,4,5]]
```

### Solution

### #1
```javascript
function chunk(array, size) {
    let res = [];

    for(let i of array){
        let lastChunk = res[res.length-1];
        
        if(!lastChunk || lastChunk.length == size){
            res.push([i]);
        }else{
            lastChunk.push(i);
        }
    }

    return res;
}

chunk([1, 2, 3, 4], 2);
```

### #2
```javascript
 function chunk(array, size) {
    let res=[];
 
    while(array.length>0){
      const chunk = array.splice(0, size);
      res.push(chunk);
    }

    return res;
};
```
