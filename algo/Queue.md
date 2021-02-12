# Queue

> A **Queue** is an ordered list of elements where an element is inserted at the end of the queue and is removed from the front of the queue.   

>**FIFO** - First In First Out

-  Linear Data Structure


The insertion operation is called **enqueue**, and the removal operation is called **dequeue**. The enqueue operation inserts an element at the end of the queue, whereas the dequeue operation removes an element from the front of a queue.


![image](https://user-images.githubusercontent.com/8204364/107130472-bfadf380-689b-11eb-8ac6-d189547e11c7.png)


### Methods
**push** - add an element to the end of queue  
**shift** - remove first element from beginning of the queue

### Solution
```javascript
class Queue {
    constructor(){
      this.data=[];
    }

    add(item){
      this.data.push(item);
    }

    remove(){
      return this.data.shift();
    }
}

const q = new Queue();
q.add(1);
q.add(2);
q.remove(); //>> Queue { arr: [ 2 ] }
```

### Resources
- <a target='_blank' href='https://www.udemy.com/course/coding-interview-bootcamp-algorithms-and-data-structure/learn/lecture/8547060'>Queue by Stephen Grider</a>
