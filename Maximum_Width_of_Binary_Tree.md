## [二叉树最大宽度](https://leetcode-cn.com/problems/maximum-width-of-binary-tree/)

层序遍历  每层队列的第一个和最后一个代表双端节点，这个我一开始没有意识到 

还有能额外定义一个结构体是最骚的  窃以为太不简洁了  哎，但是没办法  想了半天也想不出更优雅的解法

还有新结构体里面的pos，当树节点足够多的时候，**pos的值会溢出**，这个在测试用例中没有体现，但是在实际中需要注意 



### 代码实现

```go
type node struct {
	pos  int
	root *TreeNode
}

func widthOfBinaryTree(root *TreeNode) int {
	myRoot := node{1, root}
	queue := []*node{&myRoot}
	ans := 0
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	for len(queue) > 0 {
		l := len(queue) - 1
		ans = max(ans, queue[l].pos-queue[0].pos+1)
		for i := 0; i <= l; i++ {
			root = queue[0].root
			pos := queue[0].pos
			queue = queue[1:]
			if root.Left != nil {
				queue = append(queue, &node{2 * pos, root.Left})
			}
			if root.Right != nil {
				queue = append(queue, &node{2*pos + 1, root.Right})
			}
		}
	}
	return ans
}
```

