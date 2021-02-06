# Spiral Matrix
Write a function that accepts an integer N and returns a NxN spiral matrix.

```javascript
//Examples: 
matrix(2)
    [[1, 2],
     [4, 3]];

matrix(3)
    [[1, 2, 3], 
     [8, 9, 4], 
     [7, 6, 5]];

matrix(4)
    [[ 1,  2,  3, 4],
     [12, 13, 14, 5],
     [11, 16, 15, 6], 
     [10,  9,  8, 7]];
```

### Solution

```javascript
function matrix(n) {
    const res = [];
    const size = n * n;

    //create matrix
    for (let i = 0; i < n; i++) {
        res.push([]);
    }

    //fill matrix
    let dir = 'right';
    let row = 0;
    let idx = 0;

    for (let i = 1; i <= size; i++) {
        if (dir == 'right') {
            res[row][idx] = i;
            if (idx < n - 1 && !res[row][idx + 1]) idx++;
            else {
                row++;
                dir = 'down';
            }
        } else if (dir == 'down') {
            res[row][idx] = i;
            if (row < n - 1 && !res[row + 1][idx]) row++;
            else {
                idx--;
                dir = 'left';
            }
        } else if (dir == 'left') {
            res[row][idx] = i;
            if (idx > 0 && !res[row][idx - 1]) idx--;
            else {
                row--;
                dir = 'up';
            }
        } else if (dir == 'up') {
            res[row][idx] = i;
            if (!res[row - 1][idx]) row--;
            else {
                idx++;
                dir = 'right';
            }
        }
    }

    return res;
}
```
