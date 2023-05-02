# Two Pointers Technique


https://leetcode.com/articles/two-pointer-technique/


- <b>Simple</b>: pointer 1 and pointer 2 gap equal 1 step;
- <b>Slow and Fast</b>: Gap between pointer1 and pointer2 is more than 1 step. 

<img width='500' src='https://media.geeksforgeeks.org/wp-content/uploads/Floyd-Proof.jpg'/>

## When to use
- calculate mid point of an array, linked list. (Also could be used to identify 1/3, 1/4, etc)
- compare consecutive numbers 

# Simple

---

> Compare consecutive numbers

pointer 1 and pointer 2 gap equal 1 step.



    
    


### Ex 1:
Given an array of integers. Find the last number in the sequence.  

```javascript
const arr = [1,2,3,5,6];

Step 1: p1=1, p2=2
Step 2: p1=2, p2=3
Step 3: p1=3, p2=5 (!)
```  



on step 3 we see that 3 +1 != 5, thereof 3 is the final integer in the sequence.

### Ex 2:
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

##### Solution
>Time Complexity: O(N), where N is the length of the array.
```javascript
const formatArr = (arr)=>{
    arr = arr.sort((a,b)=>(a-b)); //sort array
    
    const res=[];
    let start=null; //pointer

    for(let [i, curr] of arr.entries()){
        let next=arr[i+1];
        if(!start) start = curr; //define initial number of range

        //if next != current value +1, then sequence is broken
        if(next != curr+1){
            res.push([start, curr]);
            start=null;
        }
    }

    return res;
}
const newArr = formatArr(arr);
```
 
#Slow and Fast

---

#### Ex 1: Remove Duplicates from Sorted Array
Given a sorted array nums, remove the duplicates in-place such that each element appears only once and returns the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.  

Return length of final array;

#### Solution
```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var removeDuplicates = function(nums) {
    let n=0;
    
    while(n<nums.length){
      let curr=nums[n];
      let next=nums[n+1];

    if(curr == next){
        nums.splice(n+1, 1);    
    }else{
         n++;
        curr  = nums[n];
        next  = nums[n+1];
        }
    }
    
    return nums.length;
};

const arr = [0,0,1,1,1,2,2,3,3,4];
const x = removeDuplicates(arr); // [ 0, 1, 2, 3, 4 ]
```

### Ex.2 Midpoint of the Linked List (Slow & Fast)
Return the 'middle' node of a Linked List. If the List has an even number of elements, return the node at
the end of the first half of the list.

**Do not** :
- use a counter variable,   
- retrive the size of the list, and only iterate through the list one time.
```javascript
//Example:
{a}=>{b}=>{c}  //b is a midpoint
{a}=>{b}=>{c}=>{d}  //b is a midpoint
```

```javascript
function midpoint(){
  let slow = list.head;
  let fast = list.head;

  while(fast.next && fast.next.next){
    slow = slow.next;
    fast = fast.next.next;
  }
return slow;
}
```


### Ex.3 Validate Circular Linked List (Slow & Fast)
Return false if slow and fast pointers never points to same Node and Tail was reached;
```javascript
function isCircular(list){
  let slow=list.head;
  let fast=list.head;

  while(fast.next && fast.next.next ){
    slow = slow.next;
    fast = fast.next.next;

    if(slow === fast) return true; //compare excluding initial point
  }
  return false;
}
```


## Practice
- <a target='_blank' href='https://leetcode.com/tag/two-pointers/'>LeetCode: two pointers</a>




## Resoucres
- <a target='_blank' href='https://leetcode.com/articles/two-pointer-technique/'>LeetCode</a>
- <a target='_blank' href='https://www.geeksforgeeks.org/two-pointers-technique/'>GeeksForGeeks</a>
