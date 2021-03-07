## [分割回文串](https://leetcode-cn.com/problems/palindrome-partitioning/)

用回溯不难，就是回溯时间和空间消耗都挺大



### 代码实现

```go
func partition(s string) [][]string {
	ans := make([][]string, 0)
	n := len(s)
	var dfs func(path []string, depth int)
	dfs = func(path []string, depth int) {
		top := len(path) - 1
		if depth == n && isPalindrome(path[top]) {
			temp := make([]string, len(path))
			copy(temp, path)
			ans = append(ans, temp)
			return
		} else if depth == n {
			return
		}
		if top >= 0 && isPalindrome(path[top]) {
			path = append(path, s[depth:depth+1])
			dfs(path, depth+1)
			path = path[:top+1]
		}
		if top < 0 {
			path = append(path, s[depth:depth+1])
		} else {
			path[top] += s[depth : depth+1]
		}
		dfs(path, depth+1)
	}
	dfs([]string{}, 0)
	return ans
}

func isPalindrome(s string) bool {
	S := []byte(s)
	for l, r := 0, len(S)-1; l < r; l++ {
		if S[l] != S[r] {
			return false
		}
		r--
	}
	return true
}
```

