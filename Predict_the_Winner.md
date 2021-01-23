## [预测赢家](https://leetcode-cn.com/problems/predict-the-winner/)

和石子游戏一样



### 代码实现

```go
func PredictTheWinner(nums []int) bool {
	l := len(nums)
	dp := make([]int, l)
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	for i := l - 1; i >= 0; i-- {
		dp[i] = nums[i]
		for j := i + 1; j < l; j++ {
			dp[j] = max(nums[i]-dp[j], nums[j]-dp[j-1])
		}
	}
	return dp[l-1] >= 0
}
```

