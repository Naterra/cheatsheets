# Reverse Integer

#### Example:
Reverse integer 12345 to 54321

###Solution
```javascript
function reverseInt(numb)=>{
    const reversed = numb.toString().split('').reverse().join('');
    return reversed * Math.sign(numb);
}
const x = reverseInt(12345); //54321
```
