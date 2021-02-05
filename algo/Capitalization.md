# String Capitalization

Capitalize each word in the string.\
Write a function that accepts a string. The function should capitalize the first letter of each word in the string and return the result.

```javascript
capitalize('a short sentence') --> "A Short Sentence"
capitalize('a lazy fox') --> 'A Lazy Fox'
capitalize('look, it is working!') --> 'Look, It Is Working!'
```

### Solution

```javascript
function capitalize() {
    const arr = str.split(' ');

    for (let idx in arr) {
        arr[idx] = `${arr[idx][0].toUpperCase()}${arr[idx].slice(1)}`;
    }

    return arr.join(' ');
}
```
