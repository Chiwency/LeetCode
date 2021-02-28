## [二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

因为后续遍历是第三次访问的时候才记录值 所以在出栈时判断是否是第一次出栈，如果是第一次出栈，迭代`root`后再把原节点入栈，第二次出栈就真正出栈，记录值

根据前驱节点`prev`判断是否是第一次出栈



### 代码实现

```go
func postorderTraversal(root *TreeNode) []int {
	stack := make([]*TreeNode, 0)
	ans := make([]int, 0)
	var prev *TreeNode
	for root != nil || len(stack) > 0 {
		if root != nil {
			stack = append(stack, root)
			root = root.Left
			continue
		}
		top := len(stack) - 1
		root = stack[top]
		stack = stack[:top]
		if root.Right == nil || root.Right == prev {
			ans = append(ans, root.Val)
			prev = root
			// 防止下一次有继续向左子树遍历
			root = nil
		} else {
			// 核心代码 下次又要继续跳回原来的地方,相当于不出栈
			stack = append(stack, root)
			root = root.Right
		}
	}

	return ans
}
```

