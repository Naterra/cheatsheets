# Max Chars Problem

Given a string, return the character that is most commonly used in the string


### Solution
Using the string characters, create a hash table.

![image](https://user-images.githubusercontent.com/8204364/106912763-55495780-66d1-11eb-9cc3-c3fffe5ac6d5.png)

### #1
Two loops
```javascript
function maxChar(str){
    const hMap={};

    //fill hash table
    for(let ch of str){
        hMap[ch] ? hMap[ch]++ : hMap[ch] = 1;
    }

    //filter entries
    const filtered =  Object.entries(hMap).reduce((acc, curr)=>{
        if(!acc) return curr;
        return curr[1] > acc[1] ? curr : acc;
    });

    return filtered[0];
}
```

### #2
Single loop
```javascript
 var maxChar = function(str) {
    const hMap={};
    let maxChar =null;

    for(let ch of str){
        hMap[ch] ? hMap[ch]++ : hMap[ch] = 1;
         if(maxChar && maxChar['val']< hMap[ch])  maxChar={'ch':ch, val:hMap[ch]};
         if(!maxChar) maxChar={'ch':ch, val:hMap[ch]};
    }
 
    return maxChar['ch'];
};
 
```
