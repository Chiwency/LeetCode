## [替换后的最长重复字符](https://leetcode-cn.com/problems/longest-repeating-character-replacement/)

第一次写滑动窗口，看了下[精选题解]([替换后的最长重复字符](https://leetcode-cn.com/problems/longest-repeating-character-replacement/))，讲滑动窗口，发现是真的香啊，简单易懂、

一开始还想用动规来写的，，



### 代码实现

```go
func characterReplacement(s string, k int) int {
	S := []byte(s)
	n := len(S)
	alph := make([]int, 26)
	maxInWin := 0
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	l := 0
	for r := 0; r < n; r++ {
		alph[S[r]-'A']++
		maxInWin = max(maxInWin, alph[S[r]-'A'])
		if r-l+1 > maxInWin+k {
			alph[S[l]-'A']--
			l++
		}
	}
	return n - l
}
```

