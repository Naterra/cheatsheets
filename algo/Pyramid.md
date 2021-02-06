# Pyramid

Write a function that accepts a positive number N.  
The function should console log a pyramid shape with N levels using the # character. Make sure the pyramid has spaces on both the left  and right sides.

```javascript
Example:
pyramid(1)
    '#'
pyramid(2)
    ' # '
    '###'
pyramid(3)
    '  #  '
    ' ### '
    '#####'
```

### #1 - Solution

```javascript
function pyramid(n){
    for(let i=1; i<=n; i++){
        const symb = '#'.repeat(i * 2 -1);
        const space = ' '.repeat(n-i);
        console.log(space+symb+space);
    }
}
pyramid(5);
```

### #2 - Recursive Solution

```javascript
function pyramidR(n, row=1){
    const symb = '#'.repeat(row * 2 -1);
    const space = ' '.repeat(n-row);
    console.log(space+symb+space);
    if(row<n){
      row++;
      pyramidR(n, row);
    }
}
pyramidR(4);

//    #
//   ###
//  #####
// #######
```
