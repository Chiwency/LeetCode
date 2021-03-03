## 模糊坐标

这个算分治算法吧？？？ 自然而然想到 也没看题解了 太麻烦  

关键是想通怎么判断数字合理，逗号分割 分组判断



### 代码实现

```go
func ambiguousCoordinates(S string) []string {
	s := []byte(S[1 : len(S)-1])
	ans := []string{}
	n := len(s)
	for i := 0; i < n-1; i++ {
		l := combination(s[0 : i+1])
		r := combination(s[i+1:])

		for _, s1 := range l {
			for _, s2 := range r {
				ans = append(ans, "("+s1+", "+s2+")")
			}
		}
	}
	return ans
}

func combination(s []byte) []string {
	n := len(s)
	ans := []string{}
	for i := 0; i < n; i++ {
		commas := "."
		if i == n-1 {
			commas = ""
		}
		if isValid(s[:i+1], s[i+1:]) {
			ans = append(ans, string(s[:i+1])+commas+string(s[i+1:]))
		}
	}
	return ans
}

func isValid(s1, s2 []byte) bool {
	if (len(s1) >= 2 && s1[0] == '0') || len(s2) > 0 && (s2[len(s2)-1] == '0') {
		return false
	}
	return true
}
```

