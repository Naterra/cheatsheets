# Fibonacci

>Fibonacci sequence - is a series of numbers in which each number is the sum of the two preceding numbers.   
> 
> [0,1,1,2,3,5,8,13,21] - fibonacci sequence

> Find value at index:   F(idx) = F(idx-1) + F(idx-2)



### Complexity

|       |Iterative solution|Recursive solution|Memoization|
|-------|------------------|------------------|-----------|
| Time  | O(n)             | 2^N              | 2N        |
| Space |                  |                  | O(2n)     |


### #1. Implement Fibonacci sequence up to given number (Iterative solution)

```javascript
// O(n) time complexity
function fib(n){
  let arr = [0, 1];
  for (let i = 2; i<= n; i++){
      arr.push(arr[i - 2] + arr[i -1]);
  }
 return arr;
}

fib(8); //[0,1,1,2,3,5,8,13,21]
```




### #2. Return an N-th element in Fibonacci sequence (Iterative solution)
Given a number N return the index value of the Fibonacci sequence

```javascript
// O(n) time complexity
function fib(n){
    const series=[0,1];

    for(let i=2; i<=n; i++){
        let f1 = series[i-1];
        let f2 = series[i-2];
        series.push(f1+f2);
    }

    return series[n];
}

fib(6); //8
```


### #3. Calculate the previous 2 numbers for given N(index) number (Iterative solution)
```javascript
// O(n) time complexity
function fibonacci(idx){
  let arr = [0,1];
  
  for (let i = 2; i<=idx; i++){
     arr.push(arr[i-2] + arr[i-1])
  }
 return `${arr[idx-2]}, ${arr[idx-1]}`;
}

fibonacci(5); // "2, 3"
```

### #4. Recursive solution  / 2^N Exponential Time complexity
```javascript
function fib(n) {
  if (n < 2) return n;
  return fib(n - 1) + fib(n - 2);
}
fib(5); //8
```

![image](https://user-images.githubusercontent.com/8204364/107128583-d6991980-688c-11eb-9b5f-3a9f2109dda9.png)

### #5. Memoization
> Is an optimization technique used primarily to speed up computer programs by storing the results of expensive function calls.

Exponential time complexity for recursive solution can be improved using a 
memoization. Therefore fib(n) would not re-calculate whole sequence again and again,
instead, return stored value.


Basically, if we just store the value of each index in a hash, we will avoid the computational
time of that value for the next N times. This change will increase the space complexity of our 
new algorithm to **O(n)** but will dramatically decrease the time complexity to **2N** which will resolve 
to linear time since 2 is a constant.

```javascript
//Time - O(n)
//Space - O(2n)
function fib(n, memo={}){
    if (memo[n]) return memo[n];
    if (n == 0) return 0;
    else if (n == 1) return 1;

    return memo[n] = fib(n - 1, memo) + fib(n - 2, memo);
}
const x = fib(6); //8
```
