## [统计字典序元音字符串的数目](https://leetcode-cn.com/problems/count-sorted-vowel-strings/)

刚学回溯算法，用回溯算法写，和全排列思想一样



### 代码实现

```go
func countVowelStrings(n int) int {
	ans := 0
	var dfs func(path []int)
	dfs = func(path []int) {
		l := len(path) - 1
		if l == n {
			ans++
			return
		}
		i := 0
		if l >= 0 {
			i = path[l]
		}
		for ; i <= 5; i++ {
			path = append(path, i)
			dfs(path)
			path = path[:len(path)-1]
		}
	}
	dfs([]int{1})
	return ans
}
```

