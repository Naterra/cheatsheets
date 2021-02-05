# Warm Up
Practice common data type/structure problems.  
Copy and paste tasks into your favorite IDE or use <a target='_blank' href='https://repl.it'>Repl.it</a>


## Strings
```javascript
const string = 'The quick brown fox jumps over the lazy dog.';

//1) Find length of string
 string.length;

//2) Find if string includes  'fox';
 string.includes('fox') ? true : false;

//3) Get array of words from string;
string.split(' ');

//4) Remove whitespaces from (start,end) of string;
string.trim();

//5) Extract substring between index 2 and 4

//6) Find index of substring
const idx = string.indexOf('fox'); //16

//7) Extract substring 'fox' from 'my fox' 
const s  = 'fox';
const start = string.indexOf(s); //find the index of first letter of substring
const end = start + s.length; //find the index of last letter of substring
const subString = string.substring(start, end); //extract substring


//8) repeat string 'apple' 3 times
'apple'.repeat(3);

//9) concat 2 strings 
const str1='Hello';
const str2='World';
str1.concat(' ', str2); //'Hello World'

//10) Find non word characters in string
string.match(/[\W]/g); //[' ',' ',...,'.']

//11) Replace 'fox' to 'cat'
string.replace('fox', 'cat');//'The quick brown cat jumps over the lazy dog.'


//12) Replace all substring occurrences in string
const str2 = 'Oh Mary, Mary!'; //to be 'Oh Larry, Larry!'
str2.replaceAll('Mary', 'Larry');

//13) Replace character at index  
const idx = 1;
let s = 'Hello World'; //to 'Wello World'

String.prototype.replaceCharAt = function(idx, newChar){
    return this.substring(0, idx)+newChar+this.substring(idx+newChar.length);
}
console.log(str.replaceCharAt(0, 'W'));

```


 
## Array
```javascript
const numbersArr = [5, 4, 10, 11, 0, -10, -5];
const fruitsArr = ['mango', 'banana', 'apple'];

const users=[
    {name:'Stiven', age:10},
    {name:'Mary', age:20}, 
    {name:'Nicole', age:2}
];


//1)Insert item at beginning of array
fruitsArr.unshift('cherry');

//2)Remove item from beginning  of array
fruitsArr.shift();

//3)Insert item at the end  of array
fruitsArr.push('cherry');

//4)Remove item at the end  of array
fruitsArr.pop();

//5)Remove item/s by value. For example: remove 'banana'
const newArr = fruitsArr.filter(item=>item !== 'banana');

//6)Remove item at index
const idx = 0;
fruitsArr.splice(idx,1);

//7)Replace item at index = 0 with new value 'carrot'
fruitsArr[0] = 'carrot';
//or
fruitsArr.splice(0,1,'carrot');


 
//9)Swap two items ['mango', 'banana', 'apple'] to [ 'apple', 'banana','mango']
Array.prototype.swap = function(item1, item2){
    const idx1 = this.indexOf(item1);
    const idx2 = this.indexOf(item2);
    this[idx1] = item2;
    this[idx2] = item1;
    return this;
}

fruitsArr.swap('mango', 'apple'); // [ 'apple', 'banana','mango']


/************** Find **************/
//1)Find index of item  'mango' in array
const x = fruitsArr.findIndex(item=>item=='mango'); //0
const y = fruitsArr.indexOf('mango'); //0

//2)Find index of item in users  array where item.age == '20'
const x = users.findIndex(item=>item.age=='20'); //1  returned first occurance




/************** Sort **************/
//1) Reverse an array
fruitsArr.reverse();

//2) Sort array of strings (ascending, descending).
fruitsArr.sort();

//3) Sort array of numbers (ascending, descending).
numbersArr.sort(); //wont work correctly, produce [-10,-5,0,10,11,4,5]
numbersArr.sort((a,b)=>a-b); //ascending [-1,0,1]
numbersArr.sort((a,b)=> b-a); //descending [1,0,-1]

//4) Sort array of objects by prop value (ascending, descending)
users.sort((a,b)=>a.age-b.age);//ascending
users.sort((a,b)=>b.age-a.age);//descending


/************** Filter  **************/
//1) Find users whose age less or equal 10
const filtered = users.filter(item=>item.age<=10);

//2) Find the youngest user/s
const youngest = users.reduce((acc, curr)=>{
    if(!acc) return curr;
    return curr.age >acc.age? acc : curr;
}, null);
```

## Object
```javascript
const obj1 = { a: 1, b: 2 };

//1) Merge Objects
const obj2 = { a: 11, c: 22 };
const merged = Object.assign(obj1, obj2);
const merged2 = {...obj1, ...obj2}; //ES6

//2) Get array of object keys
const x = Object.keys(obj1); //['a', 'b']

//3) Get array of object values
const x = Object.values(obj1); //[1, 2]

//4) Get array of object entries 
const x = Object.entries(obj1); // [[a,1], [b,2]]

//5) Loop object
for(let [key, val] of Object.entries(obj)){
    //key - prop key
    //val - prop value
}

//6) Sort object {b:2,c:3,a:1} -->{a:1,b:2:c:3}
function sortObject(obj) {
    return Object.keys(obj).sort().reduce(function (result, key) {
        result[key] = obj[key];
        return result;
    }, {});
}
```

## Class

```javascript
//1) Define Class "Person"
//2) Create Setter method "userName"
//3) Create Getter method "userName"
//4) Create Static method
```



 
