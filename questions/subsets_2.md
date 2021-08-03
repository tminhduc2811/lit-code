# Subsets II
Given an integer array `nums` that may contain duplicates, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

## Example 1:
```go
Input: nums = [1,2,2]
Output: [[],[1],[1,2],[1,2,2],[2],[2,2]]
```

## Example 2:
```go
Input: nums = [0]
Output: [[],[0]]
```
## Constraints:
- 1 <= nums.length <= 10
- -10 <= nums[i] <= 10

## Solutions

```go
func subsetsWithDup(nums []int) [][]int {
    
    result := [][]int{}
    result = append(result, []int{})
    
    // sort the array
    sort.Ints(nums)
    // since nums always >= 1
    result = append(result, []int{nums[0]})
    startIndex := 1
    for i:= 1; i < len(nums); i++ {
        if nums[i] != nums[i - 1] {
            startIndex = 0
        }
        for currentLength := len(result); startIndex < currentLength; startIndex++ {
            newSubset := make([]int, len(result[startIndex]))
            // we need to make a copy of the slice so the append function will not modify existing value
            copy(newSubset, result[startIndex])
            newSubset = append(newSubset, nums[i])
            result = append(result, newSubset)
        }
    }
    return result
}
```
