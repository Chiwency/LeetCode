## [不同路径](https://leetcode-cn.com/problems/unique-paths/)

动态规划问题。利用滚动数组思想，把dp数组降到一维

状态转移方程为:

```go
dp[j]=dp[j]+dp[j-1]    // 到该点路径数等于到上一点路径数dp[j]加上到左边一点的路径数dp[j-1]
```



### 代码实现

```go
func uniquePaths(m int, n int) int {
	dp := make([]int, n)
	dp[0] = 1
	for i := 0; i < m; i++ {
		for j := 1; j < n; j++ {
			dp[j] = dp[j] + dp[j-1]
		}
	}
	return dp[n-1]
}
```

**比之前有障碍的简单的多**

