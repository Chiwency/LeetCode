## [二叉树剪枝](https://leetcode-cn.com/problems/binary-tree-pruning/)

递归写比较简单



### 代码实现

```go
func pruneTree(root *TreeNode) *TreeNode {
	if !containOne(root) {
		return nil
	}
	return root
}

func containOne(root *TreeNode) bool {
	if root == nil {
		return false
	}
	l := containOne(root.Left)
	r := containOne(root.Right)
	if !l {
		root.Left = nil
	}
	if !r {
		root.Right = nil
	}
	return l || r || root.Val == 1
}
```

