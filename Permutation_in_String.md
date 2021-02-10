## [字符串的排列](https://leetcode-cn.com/problems/permutation-in-string/)

又是一道滑动窗口题，写的时候一直注意要尽量优雅

我感觉这已经是极简代码了，我可真是个小天才



### 代码实现

```go
func checkInclusion(s1 string, s2 string) bool {
	alph := [26]int{}
	S1 := []byte(s1)
	S2 := []byte(s2)
	n1 := len(S1)
	n2 := len(S2)
	for _, v := range S1 {
		alph[v-'a']++
	}

	for l, r := 0, 0; r < n2; r++ {
		if alph[S2[r]-'a'] <= 0 {
			for l <= r && alph[S2[r]-'a'] <= 0 {
				alph[S2[l]-'a']++
				l++
			}
		}
		if r-l+1 == n1 {
			return true
		}
		alph[S2[r]-'a']--
	}
	return false
}
```

