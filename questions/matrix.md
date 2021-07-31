## 01 Matrix
- Given an `m x n` binary matrix `mat`, return the distance of the nearest 0 for each cell.
- The distance between two adjacent cells is 1.

### Example
<img src="../images/01-matrix.jpg" />

Input: `mat = [[0,0,0],[0,1,0],[0,0,0]]`

Output: `[[0,0,0],[0,1,0],[0,0,0]]`

### Solution

Using dynamic programming, we can calculate the distance of current cells if we know the nearest distance of their neighbors. 
- Calculate the distance from top, left.
- Calculate the distance fromt bottom, right.

```go
func updateMatrix(mat [][]int) [][]int {
    
    rows := len(mat)
    cols := len(mat[0])
    
    result := initializeResult(rows, cols)
    
    // update top left matrix
    for rowIdx := 0; rowIdx < rows; rowIdx++ {
        for colIdx := 0; colIdx < cols; colIdx++ {
            if mat[rowIdx][colIdx] == 0 {
                result[rowIdx][colIdx] = 0
            } else {
                if rowIdx > 0 {
                    result[rowIdx][colIdx] = min(result[rowIdx][colIdx], result[rowIdx - 1][colIdx] + 1)
                }
                if colIdx > 0 && (result[rowIdx][colIdx - 1] + 1 < result[rowIdx][colIdx]) {
                    result[rowIdx][colIdx] = min(result[rowIdx][colIdx], result[rowIdx][colIdx - 1] + 1)
                }
            }
        }    
    }
    
    // After finishing the top left matrix, there are cases cannot be calculated
    for rowIdx := rows - 1; rowIdx >= 0; rowIdx-- {
        for colIdx := cols - 1; colIdx >= 0; colIdx-- {
            if rowIdx < rows - 1 {
                result[rowIdx][colIdx] = min(result[rowIdx][colIdx], result[rowIdx + 1][colIdx] + 1)
            }
            if colIdx < cols - 1 && (result[rowIdx][colIdx + 1] + 1 < result[rowIdx][colIdx]) {
                result[rowIdx][colIdx] = min(result[rowIdx][colIdx], result[rowIdx][colIdx + 1] + 1)
            }
        }
    }
    return result
}

func initializeResult(rows int, cols int) [][]int {
    max := rows + cols
    result := make([][]int, rows)
    for i := 0; i < rows; i++ {        
        c := make([]int, cols)
        for j := 0; j < cols; j++ {
            c[j] = max
        }
        result[i] = c
    }
    return result
}

func min(left int, right int) int {
    if left > right {
        return right
    }
    return left
}
```
### Solution Analysis
- Time complexity: O(rows x columns)
- Space complexity: O(1), no extra space required other than the output

<hr>


