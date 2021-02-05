# Reverse String

```javascript
const reverseString =(str)=>{
    return str.split('').reverse().join('');
}

const reverseString2 =(str)=>{
    return str.split('').reduce((rev, char) => char + rev, '');
}

reverseString('apple'); //elppa
```
