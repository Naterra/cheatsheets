# Vowels
Write a function that returns the number of vowels used in a string.
Vowels are the characters 'a', 'e', 'i','o', and 'u'.

```javascript
Example:
vovels('Hi There!') --> 3
vovels('Why do you ask?') --> 4
vovels('Why?') --> 0
```

### Solution
```javascript
function vowels(str){
    const v = str.match(/[aeiou]/g);
    return v ? v.length : 0;
}
```
