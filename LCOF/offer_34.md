## [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

​    dfs回溯，比较简单



### 代码实现

```go
/**
 * Definition for a binary tree node.
 * type TreeNode struct {
 *     Val int
 *     Left *TreeNode
 *     Right *TreeNode
 * }
 */
func pathSum(root *TreeNode, target int) [][]int {
	ans := make([][]int, 0)
	var dfs func(root *TreeNode, path []int, sum int)
	dfs = func(root *TreeNode, path []int, sum int) {
		if root == nil {
			return
		}
		sum += root.Val
		path = append(path, root.Val)
		top := len(path)
		if sum == target && root.Left == nil && root.Right == nil {
			temp := make([]int, len(path))
			copy(temp, path)
			ans = append(ans, temp)
			return
		}
		dfs(root.Left, path, sum)
		dfs(root.Right, path[:top], sum)
		return
	}
	dfs(root, []int{}, 0)
	return ans
}
```

