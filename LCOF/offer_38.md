## [剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

和数字的全排列一样，用回溯写，主要是去重，简单



### 代码实现

```go
func permutation(s string) []string {
	b := []byte(s)
	visit := make([]bool, len(b))
	ans := make([]string, 0)
	var dfs func(visit []bool, path string)
	dfs = func(visit []bool, path string) {
		if len(path) == len(b) {
			ans = append(ans, path)
		}
		temp := make([]bool, 26)
		for k, v := range b {
			if (!visit[k]) && (!temp[v-'a']) {
				temp[v-'a'] = true
				visit[k] = true
				dfs(visit, path+string(v))
				visit[k] = false
			}
		}
	}
  
	dfs(visit, "")
	return ans
}
```

