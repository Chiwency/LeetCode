## [最大层内元素和](https://leetcode-cn.com/problems/maximum-level-sum-of-a-binary-tree/)

这是一个关于**广度优先搜索**的题，主要在于如何区分每一层

### 代码

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func maxLevelSum(root *TreeNode) int {
	queue := []*TreeNode{root}
	maxSum := root.Val
	minLevel := 1 // 要求的答案
	thisLevel := 0
	for len(queue) > 0 {
		thisLevel++
        // 每次计算这层要遍历的节点数
		n := len(queue)
		// 本层节点值之和
		levelSum := 0
		// 每次读取本层的值，将下一层节点入队
		for i := 0; i < n; i++ {
			levelSum += queue[0].Val
			if queue[0].Left != nil && queue[0].Right != nil {
				queue = append(queue, queue[0].Left, queue[0].Right)
			} else if queue[0].Right != nil {
				queue = append(queue, queue[0].Right)
			} else if queue[0].Left != nil {
				queue = append(queue, queue[0].Left)
			}
			queue = queue[1:]
		}
		// 将本层节点值之和与储存的最大层值比较，如果更大，就更新
		if levelSum > maxSum {
			minLevel = thisLevel
			maxSum = levelSum
		}
	}

	return minLevel
}
```





