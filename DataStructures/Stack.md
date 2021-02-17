# Stack

> FILO - First In Last Out


![image](https://user-images.githubusercontent.com/8204364/107130842-824b6500-689f-11eb-877b-0118e040be04.png)


### Methods
**push** - add an element to the top of stack  
**pop** - remove an element from the top of stack

### Example
```javascript
class Stack{
  constructor(){
    this.items =[];
  }

  add(item){
   this.items.push(item);
  }

  remove(){
    this.items.pop();
  }

  peek(){
    return this.items[this.items.length-1]
  }
  
  clear(){
    this.items=[];
  }
};

const stack =  new Stack();
stack.add(1);
stack.add(5);
stack.remove(); //[1]
stack.clear();  //[]
 
console.log('stack', stack);
```
