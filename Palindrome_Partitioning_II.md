## [分割回文串 II](https://leetcode-cn.com/problems/palindrome-partitioning-ii/)

二维dp的动规，做过类似的，逻辑不复杂 难题中的简单题





### 代码实现

```go
func minCut(s string) int {
	S := []byte(s)
	l := len(S)
	dp := make([][]int, l)
	for i := 0; i < l; i++ {
		arr := make([]int, l)
		arr[i] = 1
		if i > 0 {
			arr[i-1] = 1
		}
		dp[i] = arr
	}
	for i := 1; i < l; i++ {
		dp[0][i] = dp[0][i-1] + 1
		for j := 0; j < i; j++ {
			if S[j] == S[i] && dp[j+1][i-1] == 1 {
				dp[j][i] = 1
				if j > 0 {
					dp[0][i] = min(dp[0][i], dp[0][j-1]+dp[j][i])
				}
			}
		}
	}
	return dp[0][l-1] - 1
}

func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}
```

