## [完全二叉树的节点个数](https://leetcode-cn.com/problems/count-complete-tree-nodes/)
 
答案是用二分查找和位运算，通过把节点索引转化为二进制快速找到第`k`个节点，很巧妙

我用的是深度优先遍历找到最后一个叶子节点，就能计算出总节点数

### 代码实现

```go
func countNodes(root *TreeNode) int {
	depth := 0
	p := root
	for p != nil {
		depth++
		p = p.Left
	}
	i := 0
	var dfs func(root *TreeNode, level int) bool
	dfs = func(root *TreeNode, level int) bool {
		if level == depth && root != nil {
			return true
		} else if root == nil {
			return false
		}
		i = i*2 + 2
		if !dfs(root.Right, level+1) {
			i -= 1
			if !dfs(root.Left, level+1) {
				i = (i - 1) / 2
				return false
			}
		}
		return true
	}
	if dfs(root, 1) {
		return i + 1
	}
	return 0
}
```

