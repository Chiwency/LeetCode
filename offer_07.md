## [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

递归大法好啊，，，，



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
func buildTree(preorder []int, inorder []int) *TreeNode {
	if len(preorder) == 0 {
		return nil
	}
	k := 0
	for k = range inorder {
		if inorder[k] == preorder[0] {
			break
		}
	}
	left := buildTree(preorder[1:k+1], inorder[:k])
	var right *TreeNode = nil
	if k != len(inorder)-1 {
		right = buildTree(preorder[k+1:], inorder[k+1:])
	}
	head := &TreeNode{
		preorder[0],
		left,
		right,
	}
	return head
}
```

