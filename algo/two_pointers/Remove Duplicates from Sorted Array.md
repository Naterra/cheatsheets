# Remove Duplicates from Sorted Array

Given a sorted array nums, remove the duplicates in-place such that each element appears only once and returns the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
 
};
```

### Solution
```javascript
function removeDuplicates(nums) {
    let n=0;

    while(n<nums.length){
        let curr=nums[n];
        let next=nums[n+1];

        if(curr == next) {
            nums.splice(n+1, 1);
        }else{
            n++;
        }
    }
    return nums.length;
};
```
