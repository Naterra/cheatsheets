



## in Loops
```javascript
const arr=['a', 'b', 'c'];
const entries = arr.entries(); //[ [0,'a'], [1,'b'], [2,'c']]
for (const [i, item] of arr.entries()) {
  console.log(i, item)
}
```
