## [单词拆分](https://leetcode-cn.com/problems/word-break/)

设`dp[j]` 表示 `s[j,l]`是否能被正确分割，状态转移方程不太标准，具体看代码

### 代码实现

```go
func wordBreak(s string, wordDict []string) bool {
	l := len(s)
	wordMap := make(map[string]int)
	for _, v := range wordDict {
		wordMap[v] = 1
	}
	dp := make([]bool, l+1)
	dp[l] = true

	for i := l - 1; i >= 0; i-- {
		for j := i + 1; j <= l; j++ {
			term := s[i:j]
			_, match := wordMap[term]
			if match && dp[j] {          // 状态转移
				dp[i] = true
				break
			}
		}
	}

	return dp[0]

}
```

