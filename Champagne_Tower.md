## [香槟塔](https://leetcode-cn.com/problems/champagne-tower/)

用时击败100%，因为用`flag`指示可以提前结束循环，提升了空间损耗



### 代码实现

```go
func champagneTower(poured int, query_row int, query_glass int) float64 {
	dp := make([]float64, query_row+1)
	dp[0] = float64(poured)
	var above, left float64
	above = 0
	left = 0
	for i := 1; i <= query_row; i++ {
		flag := true
		for j := i; j >= 0; j-- {
			if dp[j] > 1 {
				above = dp[j] - 1
			}
			if j >= 1 && dp[j-1] > 1 {
				left = dp[j-1] - 1
			}
			dp[j] = above/2 + left/2
			above, left = 0, 0
			if dp[j] > 0 {
				flag = false
			}
		}
		if flag {
			return 0
		}

	}

	if dp[query_glass] > 1 {
		return 1
	}
	return dp[query_glass]
}
```

