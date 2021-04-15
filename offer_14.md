## [剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

典型动规，用滚动数组方法优化空间，但是好像题解有O(1)的空间复杂度，，，



### 代码实现

```go
func cuttingRope(n int) int {
    if n==3{
        return 2
    }
	dp := make([]int, n+1)
	for i := 1; i <= n; i++ {
		dp[i] = i
	}
	ans := 1
	for i := 2; i < n; i++ {
		for j := i; j <= n; j++ {
			for t := 1; t <= j-i+1; t++ {
				dp[j] = max(dp[j-t]*t, dp[j])
			}
		}
		ans = max(ans, dp[n])
	}
	return ans
}

func max(a, b int) int {
	if a > b {
		return a
	}
	return b
}
```

