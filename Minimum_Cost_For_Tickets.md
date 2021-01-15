## [最低票价](https://leetcode-cn.com/problems/minimum-cost-for-tickets/)

从前往后推，状态转移方程挺好找出来的  但是后面因为`j`的边界问题，导致写的代码不够简洁 



### 代码实现

```go
func mincostTickets(days []int, costs []int) int {
	l := len(days)
	dp := make([]int, l)
	dp[0] = costs[0]
	min := func(a, b int) int {
		if a < b {
			return a
		}
		return b
	}
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}

	for i := 1; i < l; i++ {
		dp[i] = dp[i-1] + costs[0]
		// 下面只是检查能不能和前面的日子合并成7天或者30天的票
		for j := max(0, i-30); j <= i; j++ {
			if days[i]-days[j] < 7 {
				if j == 0 {
					dp[i] = min(dp[i], costs[1])
				} else {
					dp[i] = min(dp[i], dp[j-1]+costs[1])
				}
			} else if days[i]-days[j] < 30 {
				if j == 0 {
					dp[i] = min(dp[i], costs[2])
				} else {
					dp[i] = min(dp[i], dp[j-1]+costs[2])
				}
			}
		}
	}

	return dp[l-1]
}
```

