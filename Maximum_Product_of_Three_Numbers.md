## [三个数的最大乘积](https://leetcode-cn.com/problems/maximum-product-of-three-numbers/)

每日一题



### 代码实现

```go
func maximumProduct(nums []int) int {
	sort.Ints(nums)
	l := len(nums) - 1
	ans := nums[l] * nums[l-1] * nums[l-2]
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	ans = max(ans, nums[l]*nums[0]*nums[1])

	return ans
}
```

