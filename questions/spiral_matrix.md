# Spiral Matrix

Given an `m x n` matrix, return all elements of the `matrix` in spiral order.

## Example
<img src="../images/spiral1.jpg" />

```go
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [1,2,3,6,9,8,7,4,5]
```

## Solution
- Maintain 4 borders of the matrix: top, right, bottom, and left

```go
func spiralOrder(matrix [][]int) []int {
    // maintain 4 borders
    top, bottom, left, right, current := 0, len(matrix) - 1, 0, len(matrix[0]) - 1, 0
    result := make([]int, len(matrix)*len(matrix[0]))

    for top <= bottom && left <= right {
        // going from top left to top right
        for col := left; col <= right; col++ {
            result[current] = matrix[top][col]
            current++
        }
        
        if top == bottom {
            break
        }
        top++
        
        // going from top right to bottom right
        for row := top; row <= bottom; row++ {
            result[current] = matrix[row][right]
            current++
        }
        
        if right == left {
            break
        }
        right--
        
        // going from bottom right to bottom left
        for col := right; col >= left; col-- {
            result[current] = matrix[bottom][col]
            current++
        }
        
        if bottom == top {
            break
        }
        bottom--
        
        // going from bottom left to top left
        for row := bottom; row >= top; row-- {
            result[current] = matrix[row][left]
            current++
        }
        
        if left == right {
            break
        }
        
        left++
    }
    return result
}
```
