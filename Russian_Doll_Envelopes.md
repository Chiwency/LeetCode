## [俄罗斯套娃信封问题](https://leetcode-cn.com/problems/russian-doll-envelopes/)

用动态规划很好理解，感觉不像困难题



### 代码实现

```go
func maxEnvelopes(envelopes [][]int) int {
	sort.Slice(envelopes, func(i, j int) bool {
		return envelopes[i][0] < envelopes[j][0]
	})
	l := len(envelopes)
	dp := make([]int, l)
    ans := 1
	dp[0] = 1
	for i := 1; i < l; i++ {
		dp[i] = 1
		for j := i - 1; j >= 0; j-- {
			if envelopes[i][0] > envelopes[j][0] && envelopes[i][1] > envelopes[j][1] {
				dp[i] = max(dp[i], dp[j]+1)
			}
		}
        if dp[i] > ans {
            ans = dp[i]
        }
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

