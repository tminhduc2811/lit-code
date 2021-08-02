# Making A Large Island
- You are given an n x n binary matrix grid. You are allowed to change at most one 0 to be 1.
- Return the size of the largest island in grid after applying this operation.
- An island is a 4-directionally connected group of 1s.

## Example
Input:
```go
Input: grid = [[1,0],[0,1]]
Output: 3
```
### Explanation:
- Change one 0 to 1 and connect two 1s, then we get an island with area = 3.


## Solution
- Mark each island with a number as label, start with 2 because we have already used 0 and 1 in the matrix.
- Update 1 with label so we won't revisit it
```go
func largestIsland(grid [][]int) int {
    
    groupIndex := 2
    groupTotal := map[int]int{0: 0}
    
    for i := 0; i < len(grid); i++ {
        for j := 0; j < len(grid[i]); j++ {
            if grid[i][j] == 1 {
                // Set the cell's value with group label
                grid[i][j] = groupIndex

                total := 1 + 
                  markAsGroup(grid, i + 1, j, groupIndex) +                            
                  markAsGroup(grid, i - 1, j, groupIndex) + 
                  markAsGroup(grid, i, j + 1, groupIndex) + 
                  markAsGroup(grid, i, j - 1, groupIndex)

                groupTotal[groupIndex] = total
                groupIndex++
            }
        }
    }
    
    max := groupTotal[2]
    
    for i := 0; i < len(grid); i++ {
        for j := 0; j < len(grid[i]); j++ {
            if grid[i][j] == 0 {
                // golang does not support SET data structure
                groupMap := map[int]bool{}
                if i > 0 {
                    groupMap[grid[i - 1][j]] = true
                }
                if i < len(grid) - 1 {
                    groupMap[grid[i + 1][j]] = true
                }
                if j > 0 {
                    groupMap[grid[i][j - 1]] = true
                }
                if j < len(grid[0]) - 1 {
                    groupMap[grid[i][j + 1]] = true
                }
                total := 1
                for groupValue, _ := range groupMap {
                    total += groupTotal[groupValue]
                }
                max = getMax(max, total)
            }
        }
    }
    return max
}

func markAsGroup(grid [][]int, i int, j int, groupIndex int) int {
    if i < 0 || i > len(grid) - 1 || j < 0 || j > len(grid[0]) - 1 {
        return 0
    }
    if grid[i][j] == 0 || grid[i][j] > 1 {
        return 0 
    }
    grid[i][j] = groupIndex
    return 1 + 
      markAsGroup(grid, i + 1, j, groupIndex) + 
      markAsGroup(grid, i - 1, j, groupIndex) + 
      markAsGroup(grid, i, j + 1, groupIndex) + 
      markAsGroup(grid, i, j - 1, groupIndex)
}

func getMax(a int, b int) int {
    if a > b {
        return a
    }
    return b
}

```
