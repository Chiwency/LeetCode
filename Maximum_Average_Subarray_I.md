## [子数组最大平均数 I](https://leetcode-cn.com/problems/maximum-average-subarray-i/)

很简单的一道题



### 代码实现

```go
func findMaxAverage(nums []int, k int) (ans float64) {
	max := func(a, b float64) float64 {
		if a > b {
			return a
		}
		return b
	}
	var sum float64
	for i := 0; i < k; i++ {
		sum += float64(nums[i])
	}
	ans = sum
	n := len(nums)
	for i := k; i < n; i++ {
		sum = sum - float64(nums[i-k]) + float64(nums[i])
		ans = max(ans, sum)
	}
	ans /= float64(k)
	return
}
```

