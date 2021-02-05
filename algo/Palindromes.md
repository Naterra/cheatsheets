# Palindromes
>Palindromes are strings that form the same word if it is reversed.  
> 
> 'abba' => 'abba'


Given a string, return true if the string is a palindrome or false
if it is not. 


### Ex. 1
Compare string with its reversed version.
```javascript
function palindrome(str) {
    const reversed = str.split('').reverse().join('');
    return  str === reversed;
}
```

### Ex. 2
Compare characters on opposite sides of string.  
Example: ***str[0]*** and ***str[str.length -1]***

```javascript
function palindrome(str) {
   return str.split('').every((char, i)=>{
       return char === str[str.length - i -1];
   })
}
```









