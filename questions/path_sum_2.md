# Path sum II
- Given the `root` of a binary tree and an integer `targetSum`, return all `root-to-leaf` paths where each path's sum equals `targetSum`.

- A leaf is a node with no children.

## Example
<img src="../images/pathsumii1.jpg" />

```go
Input: root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
Output: [[5,4,11,2],[5,8,4,5]]

```

## Solution
- Using recursion

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func pathSum(root *TreeNode, targetSum int) [][]int {
    result := [][]int{}
    if root == nil {
        return result
    }
    if root.Left == nil && root.Right == nil {
        if root.Val == targetSum {
            return append(result, []int{root.Val})
        }
        return result
    }
    for _, path := range pathSum(root.Right, targetSum - root.Val) {
        result = append(result, append([]int{root.Val}, path...))
    }
    for _, path := range pathSum(root.Left, targetSum - root.Val) {
        result = append(result, append([]int{root.Val}, path...))
    }
    return result
}

```
