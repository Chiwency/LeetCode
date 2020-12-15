## [三角形最小路径和](https://leetcode-cn.com/problems/triangle/)

从下往上更新dp数组，状态转移方程为：

```go
dp[i]=min(dp[i-1],dp[i])+triangle[j][i]
```

代码实现：

```go
func minimumTotal(triangle [][]int) int {
	rows := len(triangle)
	if rows == 0 {
		return 0
	}
	dp := make([]int, rows+1)

	min := func(a, b int) int {
		if b < a {
			return b
		}
		return a
	}
	for j := rows - 1; j >= 0; j-- {
		colomns := len(triangle[j])
		for i := 0; i < colomns; i++ {
			dp[i] = min(dp[i], dp[i+1]) + triangle[j][i]
		}
	}

	return dp[0]
}
```



**做几题动规就开始膨胀了.......**