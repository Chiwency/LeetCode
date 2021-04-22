## [剑指 Offer 55 - I. 二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

两分钟秒了，递归比较简单



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
func maxDepth(root *TreeNode) int {
    if root==nil{
        return 0
    }
    return max(maxDepth(root.Left),maxDepth(root.Right))+1
}

func max(a,b int)int{
    if a>b{
        return a
    }
    return b
}
```

