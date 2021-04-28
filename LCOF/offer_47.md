## [剑指 Offer 47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

一开始直接用递归秒了，，，后来超时，，，

和机器人运动范围那题一样，典型的动规，还是要用动规解



### 代码实现

```go
func maxValue(grid [][]int) int {
	m := len(grid)
	n := len(grid[0])
	dp := make([]int, n)
	for i := 0; i < m; i++ {
		dp[0] += grid[i][0]
		for j := 1; j < n; j++ {
			dp[j] = max(dp[j], dp[j-1]) + grid[i][j]
		}
	}
	return dp[n-1]
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}

```

