# Tree
> A **Tree** is an abstract data type (ADT)  or data structure, that simulates a hierarchical tree structure, with a root value and subtrees of children with a parent node, represented as a set of linked nodes.

A Tree is like a linked list, except it keeps references to many child nodes in a hierarchical structure.

**Real world example of Tree: DOM (Document Object Model)**

<img width='400' src='https://user-images.githubusercontent.com/8204364/108017314-964f3f00-6fe2-11eb-9e26-faa80c91aa75.png'/>

## Types of Trees
|            | General Tree   | Binary Tree       | Binary Search Tree  | 
|------------|----------------|-------------------|---------------------|
|Child Nodes | **unlimited**  |0-2(left & right)  | 0-2(left & right)   |
|Ordered     | NO             | NO    <br/><br/> • One or both of those could be null.   | **YES**  <br/>• The value of each **left** child node must be less than its parent node.<br/>• The value of each **right** child node must be greater than its parent node               |
|| &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 1 <br> &nbsp;/ &nbsp;&nbsp; / &nbsp; \ &nbsp; \ <br> 4 &nbsp; 2 &nbsp; 10&nbsp;  0 |  &nbsp;&nbsp;&nbsp; 1 <br> &nbsp;/ &nbsp;&nbsp;&nbsp; \ <br> 55 &nbsp;&nbsp;  0 |       &nbsp;&nbsp;&nbsp; 1 <br> &nbsp;/ &nbsp;&nbsp;&nbsp; \ <br> 0 &nbsp;&nbsp;&nbsp;  2|




## General Tree Implementation
In General Tree, .add() and .remove() methods usually assigned to the Node itself. Unlike the Linked List, here we want to precisely specify on which Node we want to add or remove an element.

```javascript
class Node{
    constructor(data=null, children=[]){
        this.data = data; //stores a value.
        this.children = children; //unlimited
    }

    add(data){
        this.children.push(new Node(data));
    }
    remove(data){
        this.children = this.children.filter(node=>node.data !== data);
    }
}


class Tree{
    constructor(){
        this.root = null;
    }
}


//usage
const node = new Node(1);
const tree = new Tree();
tree.root= node;
```
 

## Tree Traversing

| Type             | Action                                                                                                              |
|------------------|---------------------------------------------------------------------------------------------------------------------|
|**Breadth-first** | start at the root, traverse each level of the tree systematically before moving on to the next level of the tree    |
|**Depth-first**   | start at the root, traverse a branch all the way down to the bottom most node or leaf node                          |

<img width='400' src="https://user-images.githubusercontent.com/8204364/108250721-922b3a80-7124-11eb-9f2f-c1a238042e35.png"/>

### Breadth-first Tree Traversing
[20]   
[0, 40,-15]   
[40,-15,  12, -2, 1, -2]   
[-15,  12, -2, 1, -2]   
[ 12, -2, 1, -2, -2]   

```javascript
traverseBF(fn){
  const arr =[this.root];  
  while(arr.length){
    const node = arr.shift();  //take first element of array
    arr.push(...node.children);//push its children at the end of arr
    fn(node);
  }
}
```

### Depth-first Tree Traversing

```javascript
traverseDF(fn){
  const arr =[this.root];
  while(arr.length){
    const node = arr.shift(); //remove first element of array
    arr.unshift(...node.children); //add its children at beginning of array
    fn(node);
  }
}
```

### Ex #1. Determine tree leves. Return number of elements at each level.
Given the root node of a tree, return an array where  each element is the width of the tree at each level.
Example:
0
/   |    \
1   2    3
|           |
4         5
Answer: [1, 3, 2]

```javascript
function levelWidth(root){
 const arr =[root, 's'];
 const counters=[0];
 
 while(arr.length>1){
   const node = arr.shift();
   if(node === 's'){
     counters.push(0);
     arr.push('s');
   }else{
     arr.push(...node.children);
     counters[counters.length -1]++;
   }
 }
 return counters;
}
```






# Binary Tree & Binary Search Tree
> A **_Binary Tree_** is a non-linear data structure in which each node can have no more than two children, which are referred to as the left child and the right child; One or both of those could also be null.

> A **Binary Search Tree (BST)** is an **ordered** binary tree. So on any subtree, the left nodes are less than the root node which is less than all of the right nodes.

Very often, when we’re talking about a binary trees we actually want to talk about a binary search trees. This ordering type makes finding a node very very fast because we have a pretty good idea where it would be.
 
<img width='400' src='https://user-images.githubusercontent.com/8204364/108251172-1a114480-7125-11eb-8357-1dc6abf757cf.png'/>




 
 

 

## Balanced and Unbalanced Bunary Search Tree
> A height-balanced binary tree is defined as a binary tree in which the left and right subtrees of every node differ in height by no more than 1.

<img width='400'  src="https://user-images.githubusercontent.com/8204364/108019144-8c7c0a80-6fe7-11eb-8c27-d7e1164722ef.png"/>

The worst nightmare for a BST is to be given numbers in order (e.g. 1, 2, 3, 4, 5, 6, 7, …). The problem here is that if we get elements in a particular order, we could get really imbalanced.

Suppose we have a new BST and we just follow the properties of insertion. So we insert one to its right and then 2 to it’s right and 3 to it’s right…. We are going to get this data structure that looks less like a tree and more like a long list. And then inserts and finding will no longer be so fast. There are some algorithms that can ensure that our tree stays balanced, that is that roughly the same number of nodes will be on the left side the subtree and on the right.





## Traversing Binary Tree

<img width='600'  src="https://user-images.githubusercontent.com/8204364/108019543-76bb1500-6fe8-11eb-9252-b6c2673a11d4.png"/>

There is three common ways we can do when walking through a tree:

| Type                   | Action                                                                                         |
|------------------------|------------------------------------------------------------------------------------------|
|**Inorder** Traversal   | Visit the left nodes first then the current node and then you go to the right nodes  |
|**Preorder** Traversal  | Visit the root first and then visit its left nodes and it’s right nodes |
|**Postorder** Traversal | The root node comes up last, so you visit the left nodes and then the right node, then the current root node|


>Typically in **binary search trees** we want to do **inorder traversals** because that actually allows the nodes to be printed in order. 


<img width='400'  src="https://user-images.githubusercontent.com/8204364/108017725-a0257200-6fe3-11eb-945c-1abd45688dca.png"/>

## Coding Binary Search Trees 

#### Node
```javascript
class Node{
    constructor(data=null, left=null, right=null){
        this.data = data;
        this.left = left;
        this.right = right;
    }
}
```

#### Tree
```javascript
class Tree{
    constructor(){
        this.root=null;
    }
}
```

### Ex#1 -Validate 
Given a node, validate the binary search tree, ensuring that every node’s left hand child is less than the parent node’s value, and that every node’s right hand child is greater than the parent

```javascript
function validate(node, min=null, max=null){
  if(max !==null && node.data >max) return false;
  if(min !==null && node.data <min) return false;
  
  if(node.left && !validate(node.left, min, node.data)) return false;
  if(node.right && !validate(node.right, node.data, max)) return false;
  
  return true;
}
```

https://medium.com/swlh/binary-search-tree-in-javascript-31cb74d8263b
https://medium.com/@eric_lum/maximum-depth-of-a-binary-tree-in-javascript-5f25dab5596b

https://medium.com/@eric_lum/maximum-depth-of-a-binary-tree-in-javascript-5f25dab5596b
