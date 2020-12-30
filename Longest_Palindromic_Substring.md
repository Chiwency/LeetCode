

## [最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

一道简单的动态规划，这样看只能是O(n2)的时间和空间复杂度，但是官方有给出其他算法能到O(n)的时间复杂度。可能在很多情况下动态规划不一定是最优解。

> 这里我写的状态转移方程比官方给的要简单一些，具体就看代码吧

### 代码实现

```go
func longestPalindrome(s string) string {
	l := len(s)
	dp := make([][]bool, l)
	for i := range dp {
		dp[i] = make([]bool, l)
		dp[i][i] = true
		if i == 0 {
			continue
		}
		dp[i][i-1] = true  // 为例避免后面 i 和 j 靠在一起的情况
	}
	result := s[0:1]
	for i := 1; i < l; i++ {
		for j := i - 1; j >= 0; j-- {
			if s[i] == s[j] {
				dp[j][i] = dp[j+1][i-1]
				if i-j > len(result)-1 && dp[j][i] {
					result = s[j : i+1]
				}
			}
		}
	}
	return result
}
```

