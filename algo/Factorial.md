# Factorial
> Factorial - product of an integer and all the integers below it;   
> factorial four ( 4! ) is equal to 24.
> 1*2*3*4 = 24

### Iterative Solution
```javascript
/**
 * @param {n number}
 * @return {number}
 */
function factorial(n){
    let res=1;
    for(let i=2; i<=n; i++){
        res = res * i;
    }
    return res;
}
```
### Recursive Solution
```javascript
function factorialR(n){
  if(n<1) return 1;
  return n * factorialR(n-1);
}
```


