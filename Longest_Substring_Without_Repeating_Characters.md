## [无重复字符的最长子串](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/)

滑动窗口，一样的套路，不是很难



### 代码实现

```go
func lengthOfLongestSubstring(s string) int {
	S := []byte(s)
	hash := make(map[byte]int)
	maxInWin := 0
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	n := len(S)
	for l, r := 0, 0; r < n; r++ {
		hash[S[r]]++
		maxInWin = max(maxInWin, len(hash))
		if r-l+1 > maxInWin {
			hash[S[l]]--
			if hash[S[l]] <= 0 {
				delete(hash, S[l])
			}
			l++
		}
	}
	return maxInWin
}
```

