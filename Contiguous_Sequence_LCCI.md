## [连续数列](https://leetcode-cn.com/problems/contiguous-sequence-lcci/)

在简单题上翻了车，居然忘了基本的动规思路，，，

还可以用贪心写，符合贪心的思想



### 代码实现

```go
func maxSubArray(nums []int) int {
	l := len(nums)
	dp := math.MinInt32
	ans := math.MinInt32
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	for i := 0; i < l; i++ {
		dp = max(dp+nums[i], nums[i])
		if dp > ans {
			ans = dp
		}
	}
	return ans
}
```

