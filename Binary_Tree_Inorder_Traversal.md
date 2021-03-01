## [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

用栈写一下中序遍历，和前序遍历基本一样  要熟练写出过程



### 代码实现

```go
func inorderTraversal(root *TreeNode) []int {
	stack := make([]*TreeNode, 0)
	ans := make([]int, 0)
	for root != nil || len(stack) > 0 {
		if root == nil {
			top := len(stack) - 1
			ans = append(ans, stack[top].Val)
			root = stack[top].Right
			stack = stack[:top]
			continue
		}
		stack = append(stack, root)
		root = root.Left
	}
	return ans
}
```

