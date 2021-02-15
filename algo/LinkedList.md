# Linked List

> The linked List is an ordered collection of data. 
> The collection contains a number of different nodes, where each Node contain some amount of data along with a reference to the next node.
>
> - Linear Data Structure 

### Tyes of Linked List
- **Singly** linked list
- **Doubly** linked list.
- **Circular** Linked List

### Structure of Linked List
- Head
- Tail
- Nodes

### Complexity
![image](https://user-images.githubusercontent.com/8204364/107839351-4e79af00-6d79-11eb-897a-67df6175f825.png)

 
 
<img width='600' src='https://user-images.githubusercontent.com/8204364/107837632-de1a6000-6d6f-11eb-9319-b1c04cea8e60.png'/>



[comment]: <> (<img width='600' src='https://user-images.githubusercontent.com/8204364/107837663-0efa9500-6d70-11eb-9f7b-c660dca9904e.png'/>)

Bellow is a very basic implementation of Linked List and Node.

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

## Singly Lnked List
Singly Lnked List is a most basic implementation.
Each node in a singly-linked list contains not only the value but also a reference field to link to the next node. By this way, the singly-linked list organizes all the nodes in a sequence.

# Common Tasks

- Add
    - Implement method **addAtHead**(val) 
    - Implement method **addAtTail**(val)
    - Implement method **addAtIndex**(index, val)
- Get
    - Implement method **getSize**()
    - Implement method **getFirst**()
    - Implement method **getLast**()
    - Implement method **get**(index)
- Remove  
    - Implement method **removeFirst**()
    - Implement method **removeLast**()
    - Implement method **deleteAtIndex**(val)
- Implement method **clear**()
- Implement custom **forEach**() method

<mark>!</mark> - While working with LL methods, be careful with cases when List has no Nodes   
<mark>!</mark> - Try to reuse existing methods where possible
<mark>!</mark> - addAtHead, addAtTail, removeFirst, removeLast is only for pricticing purpose. On real interview use addAtIndex(), deleteAtIndex()


### addAtHead()
```javascript
//make sure it would not overwrite existing data at head
addAtHead(data){
    this.head = new Node(data, this.head);
}
// LinkedList {
//      head: Node { data: 15, next: Node { data: 5, next: null } }
//  }
```

### getSize()
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

### getFirst()
Return the first node of a LL.
```javascript
getFirst(){
  return this.head;
}
```

### getLast()
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

### clear()
Clear method empties the linked List.
```javascript
clear(){
    this.head=null;
}
```

### removeFirst()
Remove first Node of LL. The Lists head now should be the second element.
```javascript
removeFirst(){
    if(!this.head) return; //prevent error
    this.head = this.head.next;
}
```

### removeLast()
Remove the last node of the chain.

<img width='600' src='https://user-images.githubusercontent.com/8204364/107842781-c2c14c00-6d93-11eb-9d77-7076ed005fb3.png'/>



#### #1. Example
```javascript
removeLast(){
    let node = this.head;

    //Loop until last node before the tail (tail.next == null)
    //While node has next prop, it is not a tail
    while(node.next){
        //If next node has no next, then it's tail
        //Set current node.next to null to define new tail 
        if(!node.next.next) node.next=null;
        else node = node.next;
    }
}
```

#### #2. Example
Use **two pointers technique**
```javascript
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

### addAtTail()
Inserts a new node with provided data at the end of the chain.

```javascript
addAtTail(val){
    //If List has no Nodes yet, set new value as a Head Node and return.
    if(!this.head){
      this.head = new Node(val);
      return;
    }

    let node = this.head;
    
    //Loop up to tail Node (tailNode.next == null)
    while(node){
      //It's a tail! Add next Node to it!  
      if(!node.next) {
        node.next = new Node(val);
        break;
      }
      
      node=node.next;
    }
}

//ha-ha, that was wrong solution, use this one instead 
addAtTail(val){
    let last = this.getLast();
    if(!last) this.head = new Node(val);
    else last.next = new Node(val);
}
```


### getAtIndex()
Returns the node at the provided index
```javascript
getAtIndex(idx){
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
### deleteAtIndex()
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

[comment]: <> (### insertAt&#40;&#41;)
### addAtIndex()
Create an insert a new node at provided index. If index is out of bounds, add the node to the end of the list

Similar to deleteAtIndex(), calculate prevNode, currentNode and assign prevNode.next to point on NewNode and NewNode.next to point at currentNode.
```javascript
addAtIndex(idx, val){
   // const newNode = new Node(val); 

   //special case when idx at head and no prevNode exist
  if(idx==0){
    this.head = new Node(val, this.head.next);
  }
  else{
    const prevNode = this.getAtIndex(idx-1) || this.getLast();
    if(!prevNode) return; //if given index exceeds List chain size
    prevNode.next =new Node(val,prevNode.next );
  }

}
```
### custom forEach() to iterate the Linked List
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

list.forEach((item, i)=>{
    ...
});
```


### custom 'for of'


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


### Midpoint of Linked List
Return the middle node of a linked list.   
If the list has an even number of elements, return the node at the end of the first half of the list.   

Do not use a counter variable, do not retrieve the size of the list, and only iterate through the list one time.


```javascript
midPoint(){
    
}
```










