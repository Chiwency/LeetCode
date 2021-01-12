## [最大二叉树](https://leetcode-cn.com/problems/maximum-binary-tree/)

用递归写，挺简单的 

需要注意的是时间复杂度的估计，数组有序是最坏的情况，是O(n2)



### 代码实现

```go
func constructMaximumBinaryTree(nums []int) *TreeNode {
	if len(nums) == 0 {
		return nil
	}
	max := 0
	for k := range nums {
		if nums[k] > nums[max] {
			max = k
		}
	}
	root := new(TreeNode)
	root.Val = nums[max]
	root.Left = constructMaximumBinaryTree(nums[:max])
	root.Right = constructMaximumBinaryTree(nums[max+1:])

	return root
}
```

