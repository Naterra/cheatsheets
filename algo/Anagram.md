# Anagram

>One string is ***anagram*** of another if it uses the same characters and in the same quantity.

#### Problem Types:
- Is valid anagram  
- Extra characters. (Count number of letters that must be removed)

## Is valid anagram
Check to see if two provided strings are anagrams of eachother.
Only consider characters, not spaces or punctuation. Consider capital letters to be the same as lowercased.

>Example:  
> anagrams('rail safety', 'fairy tales') --> True  
> anagrams('RAIL! SAFETY!', 'fairy tales') --> True  
> anagrams('Hi there', 'Bye there') --> False  

 

### #1 - Compare  strings with sorted characters by length and equality 
```javascript
function anagrams(stringA, stringB) {
  //remove space and punctuation, set lowercase
  let s1 = stringA.toLowerCase().replace(/\W/g, '');
  let s2 = stringB.toLowerCase().replace(/\W/g, '');

  //Sort
  if(s1.length == s2.length ){
    s1 = s1.split('').sort().join('');
    s2 = s2.split('').sort().join('');  
    return s1 === s2; 
  }else{
    return false;
  }
};
anagrams('rail safety', 'fairy tales') //true
```

### #2 - Compare  2 Hash Tables by key/val
> two Hash Tables considered to be equal if their:
> - ***size's***  equal
> - each ***key*** exist and its ***val*** matches

#### Steps
- Create Hash Tables using word characters only
- ***Compare their sizes***, if dont match - return false
- ***compare key/val***, if dont match - return false

```javascript
function charMap(str){
    const m={};
    for(let i of str.replace(/\W/g, '')){
        m[i] ? m[i]++ : m[i]=1;
    }
    return m;
}

function anagrams(stringA, stringB) {
  let s1 = charMap(stringA);
  let s2 = charMap(stringB);

  //if size dont match
  if(Object.keys(s1).length != Object.keys(s2).length ) return false;

  //compare key/val
  for(let [key,val] of Object.entries(s1)){
    //key should exist and its val equal
    if(!s2[key] || s2[key] !== s1[key]) return false;
  }

   return true;
};
```
### #3 Compare  2 Serialized Hash Tables  
> Serialized Hash Tables must be equal  
> a: '{"a":2,"e":1,"f":1,"i":1,"l":1,"r":1,"s":1,"t":1,"y":1}',  
> b: '{"a":2,"e":1,"f":1,"i":1,"l":1,"r":1,"s":1,"t":1,"y":1}'

#### Steps
- Create Hash Tables using word characters only
- Sort Hash Tables
- Compare strings

```javascript
function charMap(str){
    const m={};
    for(let i of str.replace(/\W/g, '')){
      m[i] ? m[i]++ : m[i]=1;
    }
    return m;
}

function sortObject(obj) {
    return Object.keys(obj).sort().reduce(function (result, key) {
        result[key] = obj[key];
        return result;
    }, {});
}

function anagrams(stringA, stringB) {
  let s1 = charMap(stringA);
  let s2 = charMap(stringB);

  let s1Sorted = sortObject(s1);
  let s2Sorted = sortObject(s2);

  return JSON.stringify(s1Sorted) ==JSON.stringify(s2Sorted);
};
```
# Extra characters.

### #1 - Count number of letters that must be removed to make Anagram valid
```javascript
/**
* If we remove all matched letters one by one from both strings,
* then only not matched characters will be left in each string.
* The amount of not matched letters in string 1 or 2 will be the answer.
**/ 
const makeAnagram = (a,b)=>{
  const aCopy = a;

  //Loop a copy of 1st str, remove matched letters from both strings
   for(let i=0; i<=aCopy.length; i++){
     const ch = aCopy[i];
     
     if(b.includes(ch)){
        a = a.replace(`${ch}`, ''); //replace - will remove only first occurance 
        b = b.replace(`${ch}`, '');
     }
   }

   return a.length + b.length;
}

makeAnagram('fox', 'box'); //1
makeAnagram('fcrxzwscanmligyxyvym', 'jxwtrhvujlmrpdoqbisbwhmgpmeoke');
```
