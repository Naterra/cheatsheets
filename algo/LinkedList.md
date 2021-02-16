# Linked List

 
> **Linked List** - is an ordered collection of data. The collection contains a number of different nodes, where each Node contain some amount of data along with a reference to the next node.
>
> **Linked list** - is a linear collection of data elements whose order is not given by their physical placement in memory.
>
> Linear Data Structure 

### Tyes of Linked List
- **Singly** linked list
- **Doubly** linked list.
- **Circular** Linked List

### Structure of Linked List
- Head
- Tail (if not Circular)
- Nodes

### Complexity
![image](https://user-images.githubusercontent.com/8204364/107839351-4e79af00-6d79-11eb-897a-67df6175f825.png)

 
 


## Hints

- Reuse class methods
- Eficiency of some methods could be improved by creating **size** and **tail** properties in the linkedList class. 


## Singly Lnked List
Singly Lnked List is a most basic implementation of Linked List.
Each node in a singly-linked list contains not only the value but also a reference field to link to the next node. By this way, the singly-linked list organizes all the nodes in a sequence.
The first node is called the head while the last node is called the tail.

<img width='500' src='https://user-images.githubusercontent.com/8204364/107837632-de1a6000-6d6f-11eb-9319-b1c04cea8e60.png'/>


### Node
```javascript
class Node{
    constructor(data, next=null){
        this.data=data;
        this.next=next;   
        // this.prev=prev; (only in Doubly Linked List)
    }
}
```
### List
```javascript
class LinkedList{
    constructor(){
        this.head=null;
    }
}

const list = new LinkedList();
list.head = new Node(10); //LinkedList { head: Node { data: 10, next: null } }
```

### Creation & Access to nodes
```javascript
// create the first node
const node = new Node(23);

// add a second node
node.next = new Node(6);

// add a third node
node.next.next = new Node(15);
```


# Common Tasks

- Add
    - Implement method **addAtHead**(val) 
    - Implement method **addAtTail**(val)
    - Implement method **addAtIndex**(index, val)
- Get
    - Implement method **getSize**()
    - Implement method **getFirst**()
    - Implement method **getLast**()
    - Implement method **getAtIndex**(index)
- Remove  
    - Implement method **removeFirst**()
    - Implement method **removeLast**()
    - Implement method **deleteAtIndex**(val)
- Implement method **clear**()
- Implement custom **forEach**() method

<mark>!</mark> - While working with LL methods, be careful with cases when List has no Nodes.    
<mark>!</mark> - addAtHead, addAtTail, removeFirst, removeLast is only for practicing purpose. On real interview use addAtIndex(), deleteAtIndex()


## List Traversal
In most cases, we will use the head node (the first node) to represent the whole list. Unlike the array, we are not able to access a random element in a singly-linked list in constant time. If we want to get the i-th element, we have to traverse from the head node one by one. It takes us O(N) time on average to visit an element by index, where N is the length of the linked list.

> {23}=>{6}=>{2}=>{3}=>{4}

For instance, in the example above, the head is the node 23. The only way to visit the 3rd node is to use the "next" field of the head node to get to the 2nd node (node 6); Then with the "next" field of node 6, we are able to visit the 3rd node.

It could be efficient to store tail reference to a node and length, to simplify addition at the end of LinkedList and getting LinkedList length in the future.



### .addAtHead()
Implement method to add Node at the head. Make sure it would not overwrite existing data at head.
```javascript
//O(1)
addAtHead(data){
    this.head = new Node(data, this.head);
}
// LinkedList {
//      head: Node { data: 15, next: Node { data: 5, next: null } }
//  }
```

### .getSize()
Returns the number of nodes in the Linked List.
```javascript
getSize(){
    let size=0;
    let node = this.head;

    while(node){
        size++;
        node = node.next;
    }
    return size;
}
```

### .getFirst()
Return the first node of a LL.
```javascript
getFirst(){
  return this.head;
}
```

### .getLast()
Return the last node of a Linked List or NULL if LL is emply.
```javascript
getLast(){
    let last=null;
    let node=this.head;

    while(node){
        if(!node.next) last =node;
        node = node.next;
    }
    return last;
}
```

### .clear()
Clear method empties the linked List.
```javascript
clear(){
    this.head=null;
}
```

### .removeFirst()
Remove first Node of Linked List. The Lists head now should be the second element.
```javascript
removeFirst(){
    if(!this.head) return; //prevent error
    this.head = this.head.next;
}
```

### .removeLast()
Remove the last node of the chain.

<img width='600' src='https://user-images.githubusercontent.com/8204364/107842781-c2c14c00-6d93-11eb-9d77-7076ed005fb3.png'/>




```javascript
// Example #1
removeLast(){
    let node = this.head;

    //Loop until last node before the tail (tail.next == null)
    //While node has next prop, it is not a tail
    while(node.next){
        //Set current node.next to null to define new tail 
        if(!node.next.next) node.next=null;
        else node = node.next;
    }
}
```

 
```javascript
// Example #2 - two pointers technique
removeLast(){
    let prev=null;
    let node=this.head;

    while(node){
      if(!node.next) prev.next=null;
      prev = node;
      node = node.next; 
    }
}
```

### .addAtTail()
Inserts a new node with provided data at the end of the chain.

```javascript
// O(N). It could be O(1) if this.tail reference was saved 
addAtTail(val){
    let node = this.head;
    
    //Loop up to tail Node (tailNode.next == null)
    while(node){
        node = node.next;
    }
    node.next = new Node(val);
}

//ha-ha, that was wrong solution, use this one instead
//As I said earlier, reuse methods where it's possible
addAtTail(val){
    let last = this.getLast();
    if(!last) this.head = new Node(val);
    else last.next = new Node(val);
}
```


### .getAtIndex()
Returns the node at the provided index
```javascript
//O(N)
getAtIndex(idx){
  if(idx < 0) return null;
  let node = this.head;
  let n=0;

  //dont forget to check existence of node. Given index could be bigger than List size
  while(node && n<=idx){
    if(n==idx) return node; //node at idx found
    else{
      node = node.next;
      n++;
    }
  }
}
```

[comment]: <> (### removeAt&#40;&#41;)
### .deleteAtIndex()
Removes node at the provided index.   

For example, removing Node at index=1 could be implemented by assigning new next value to previous Node. 
Remove **Blue** at index 1:  
list[0].next (green) instead of pointing to list[1] (blue) should point to list[2] (red).
 
> list[0].next = list[2]    
> or   
> list[0].next = list[1].next

 

<img width='600' src='https://user-images.githubusercontent.com/8204364/107845010-4ab05180-6da6-11eb-801e-18f32c816a12.png'/>


```javascript
deleteAtIndex(idx){
    if(idx==0) this.head = this.head.next; //special case when idx at head
    else{
        const prevNode = this.getAtIndex(idx-1);
        //assign nextNode value to PrevNode.next, thereof current Node will be removed from the chain
        //Always check for current Node existence!
        if(prevNode && prevNode.next) prevNode.next = prevNode.next.next;
    }
}
```


### .addAtIndex()
Create and insert a new node at provided index. If index is out of bounds, add the node to the end of the list

Similar to deleteAtIndex(), calculate prevNode, currentNode and assign prevNode.next to point on NewNode and NewNode.next to point at currentNode.
```javascript
addAtIndex(idx, val){
   //special case when idx at head and no prevNode exist
  if(idx==0) this.head = new Node(val, this.head.next);
  
  else{
    const prevNode = this.getAtIndex(idx-1) || this.getLast();
    if(!prevNode) return; //if given index exceeds List chain size
    prevNode.next = new Node(val,prevNode.next );
  }
}
```
### .update()
Update value at index, return undefeined if index not exist
```javascript
update(idx, val){
  let node = this.getAtIndex(idx);
  if(node) node.val = val;
}
```
 
  
  


## Implement custom forEach() to iterate the Linked List
Calls the provided function with every node of the chain and the index of the node.
```javascript
forEach(fn){
  let node = this.head;
  let counter = 0;

  while(node){
    fn(node, counter);
    node =node.next;
    counter++;
  }
}

list.forEach((item, i)=>{ ...});
```


## Implement custom 'for of' to iterate the Linked List

- <a href='https://www.udemy.com/course/coding-interview-bootcamp-algorithms-and-data-structure/learn/lecture/8547194#overview'>Generators/Stephen Grider</a>

```javascript
class LinkedList{
    ...
    *[Symbol.iterator](){
        let node = this.head;

        while(node){
            yield node;
            node = node.next;
        }
    }
    ...
}

//usage
for(let node of list){
    console.log({node});
}
```




## Find Midpoint of Linked List
Return the middle node of a Linked List. If the list has an even number of elements, return the node at the end of the first half of the list.   

**Do not** :
- use a counter variable,
- retrive the size of the list, and only iterate through the list one time.
```javascript
//Example:
{a}=>{b}=>{c}  //b is a midpoint
{a}=>{b}=>{c}=>{d}  //b is a midpoint
```

```javascript
function midpoint(list){
    let slow = list.head;
    let fast = list.head;

    while(fast.next && fast.next.next){
        slow = slow.next;
        fast = fast.next.next;
    }
    return slow;
}
```
**Explanation**:   
We can use a **two pointers technique**. 'Slow' pointer will move 1 step at a time, while 'Fast' pointer -2 steps at a time.
In this case, when 'Fast' reaches the end of the list, 'Slow' pointer would stop in the middle.


## Return the Node places N spaces from the Tail  
Given a Linked List and integer n, return the element n spaces from the last Node in the list.
Do not call the 'size' method of the linked list. Assume that n will always be less than the length of the list.

>Example:   
> list: [a]=>[b]=>[c]=>[d],    
> n:2  
> return: [b]

### Solution:
- **two pointers technique**
  
It doesn't necessary that 'slow' and 'fast' suppose to move instantly with some specific distance between them. 
In this particular case, we even can't configure ahead 'fast' value. But, we can let it go until it moves **N** spaces ahead of 'slow'.
As soon as our 'slow' delays on **N steps**, it can move ahead either.

When loop reach the last element of the Linked List, 'slow' will point on right Node (n spaces from the last Node ).  


```javascript
function fromLast(list, n){
    let slow  = list.head;
    let fast  = list.head;   
    let i=0;

    while(fast){
      if(!fast.next) return slow;
      if(i>=n) slow = slow.next; //increase with delay
      fast = fast.next;
      i++;
    }
    return slow;
}
```

```javascript
//other aproach
function fromLast(list, n){
  let slow  = list.head;
  let fast  = list.head;
  
  //move 'fast' ahead on N spaces
  while(n>0){
      fast = fast.next;
      n--;
  }
  
  //move them together 
  while(fast.next){
    slow  = slow.next; 
    fast  = fast.next; 
  }
}
```
<mark>!</mark> Both solutions O(n) - Linear Time complexity


## Reverse Linked List in place
Reverse Linked List in place and return new head.

**in-place algorithm** is an algorithm which transforms input using no auxiliary data structure. However, a small amount of extra storage space is allowed for auxiliary variables.

```javascript
//O(n) traversing the list only once
//Space O(1) because our approach is reversing the list in place and not using any additional space
function reverseList(head) {
  let current =  head;
  let next = null;
  let prev = null;

  while(current){
    next = current.next;
    current.next = prev;

    prev = current;
    current = next;
  }
  return prev;
};
```


# Circular Linked List

---

[comment]: <> (<img src='https://user-images.githubusercontent.com/8204364/107897798-15237980-6f08-11eb-9ab1-ad1768722556.png'/>)

<img width='500' src='https://user-images.githubusercontent.com/8204364/107897851-3a17ec80-6f08-11eb-8111-5619e6f94a11.png'/>

### Specification
- no tail


### Creation
```javascript
const a = new Node('a');
const b = new Node('b');
const c = new Node('c');
const l = new List();
l.head = a;
a.next = b;
b.next = c;
c.next = b;
```


### #1 - Validate Circular Linked List
Given a linked List, return true if the list is circular, false if it is not.

**Solution:** We can use **two pointers technique (slow/fast)** to determine if the linked List is circular.

Both pointers will start at head. 'Slow' with one step at a time and 'Fast'- with 2 steps at a time. 
If list is circular, both pointers will meet each other at same Node. If Linked List is not circular, then 'Fast' discover tail with next=null, and we return false in that case.


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

# Doubly linked list

<img width='400' src='https://user-images.githubusercontent.com/8204364/107905761-79046d00-6f1d-11eb-8309-f1d37da7abcf.png'/>

Doubly linked list is a type of List where each Node has pointer to next and prev node.

### Node
```javascript
class Node{
    constructor(data, next=null, prev=null){
        this.data=data;
        this.next=next;   
        this.prev=prev;  
    }
}
```


# Practice
- [Reverse Singly Linked list / LeetCode](https://leetcode.com/problems/reverse-linked-list/)
- [Reverse Singly Linked list between position n and m/ LeetCode](https://leetcode.com/problems/reverse-linked-list-ii/)
- Flatten a Multilevel Doubly Linked List / LeetCode


# Resources
- [Linked List / Stephen Grider](https://www.udemy.com/course/coding-interview-bootcamp-algorithms-and-data-structure/learn/lecture/8547202#notes)
