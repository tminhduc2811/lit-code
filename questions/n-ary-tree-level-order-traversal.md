# N-ary Tree Level Order Traversal
Given an n-ary tree, return the level order traversal of its nodes' values.

Nary-Tree input serialization is represented in their level order traversal, each group of children is separated by the null value (See examples).

## Example 1
<img src="../images/narytreeexample.png" />

```go
Input: root = [1,null,3,2,4,null,5,6]
Output: [[1],[3,2,4],[5,6]]
```
<img src="../images/sample_4_964.png" />

```go
Input: root = [1,null,2,3,4,5,null,null,6,7,null,8,null,9,10,null,null,11,null,12,null,13,null,null,14]
Output: [[1],[2,3,4,5],[6,7,8,9,10],[11,12,13],[14]]
```

## Solution
```go
/**
 * Definition for a Node.
 * type Node struct {
 *     Val int
 *     Children []*Node
 * }
 */

func levelOrder(root *Node) [][]int {
    result := [][]int{}
    if root != nil {
        result = traverse([]*Node{root}, 0, result)
    }
    return result
}

func traverse(nodes []*Node, level int, result [][]int) [][]int {
    if len(result) <= level && len(nodes) > 0 {
        result = append(result, []int{})
    }
    if len(nodes) > 0 {
        for _, node := range nodes {
            result[level] = append(result[level], node.Val)
            result = traverse(node.Children, level + 1, result)
        }
    }
    return result
}
```
