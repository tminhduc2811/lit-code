# Two Sum
- Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
- You may assume that each input would have exactly one solution, and you may not use the same element twice.
- You can return the answer in any order.

## Example

```go
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].
```

## Solution:
```go
func twoSum(nums []int, target int) []int {
    m := map[int]int{}
    
    for i := 0; i < len(nums); i++ {
        subtracted := target - nums[i]
        if v, ok := m[subtracted]; ok {
            return []int{v, i}
        } else {
            m[nums[i]] = i
        }
    }
    return []int{}
}
```