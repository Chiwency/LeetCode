## [解码方法](https://leetcode-cn.com/problems/decode-ways/)

状态转移方程很容易想出来，主要是一些限制条件比较麻烦

**注意`string`中的元素是`rune8`类型，强制类型转换`int(s[i])`不一定是按照`ASCII码`来的，在该题中就出错了。**

直接贴代码

### 代码实现

```go
func numDecodings(s string) int {
	l := len(s)
	dp := make([]int, l+1)
	if s[0] == '0' {
		return 0
	}
	if s[l-1] != '0' {
		dp[l-1] = 1
	}
	dp[l] = 1

	for i := l - 2; i >= 0; i-- {
		m, _ := strconv.Atoi(string(s[i]))
		t, _ := strconv.Atoi(string(s[i+1]))
		n := m*10 + t
		if m == 0 {
			dp[i] = 0
		} else if n >= 10 && n <= 26 {
			dp[i] = dp[i+1] + dp[i+2]
		} else {
			dp[i] = dp[i+1]
		}
	}
	return dp[0]
}
```

