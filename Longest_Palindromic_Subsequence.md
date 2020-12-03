## 最长回文子序列

> https://leetcode-cn.com/problems/longest-palindromic-subsequence

  设子序列为（s[i].....s[j]） 设``dp[i][j]`` 为对应子序列的最长回文串长度

状态转移方程为：

```go
if s[i] == s[j]
    dp[i][j] = dp[i + 1][j - 1] + 2;
else
    dp[i][j] = max(dp[i + 1][j], dp[i][j - 1]);
```



### 代码实现

```go

func longestPalindromeSubseq(s string) int {
	l := len(s)
	// 创建多维切片的奇技淫巧
	dp := make([][]int, l)
	for i := 0; i < l; i++ {
		dp[i] = make([]int, l)
	}
    // leetcode里学的
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	// 初始化状态，左右边界相等（子序列长度为1）的时候回文序列长度为1
	// 其他为0
	for i := 0; i < l; i++ {
		dp[i][i] = 1
	}
	// 分析例子，结合状态转移方程就可以发现左边界只能从最后开始回退
	for i := l - 1; i >= 0; i-- {
		for j := i + 1; j < l; j++ {
			if s[i] == s[j] {
				dp[i][j] = dp[i+1][j-1] + 2
			} else {
				dp[i][j] = max(dp[i+1][j], dp[i][j-1])
			}
		}
	}

	return dp[0][l-1]
}
```



**动态规划进展（2/N），对于动态规划，设计dp数组（一维还是二维）,找对状态转移方程很重要!!!!**