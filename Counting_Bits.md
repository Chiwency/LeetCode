## [Counting Bits](https://leetcode-cn.com/problems/counting-bits/)

位运算加动态规划，想到状态转移方程就很好解了



### 代码实现

```go
func countBits(num int) []int {
	if num == 0 {
		return []int{0}
	}
	dp := make([]int, num+1)
	dp[0] = 0
	dp[1] = 1
	for i := 1; i < num; i++ {
		if (i&1)^1 == 1 {
			dp[i+1] = dp[i>>1] + 1
		} else {
			dp[i+1] = dp[i>>1+1]
		}
	}
	return dp
}
```

