# Steps
Write a function that accepts a positive number N.  
The function should console.log a step shape with N levels using the # character. Make sure the step has spaces on the right hand side!

```javascript
Example:
steps(2)
    '# '
    '##'
steps(3)
    '#  '
    '## '
    '###'
```

## Solution

### #1 - Loop
```javascript
function steps(n){
  for(let i=1; i<=n; i++){
    const symb = '#'.repeat(i);
    const spaces = ' '.repeat(n-i);
    console.log(symb+spaces);
  }
}
steps(4);
```
### #2 - Recursion
```javascript

```
