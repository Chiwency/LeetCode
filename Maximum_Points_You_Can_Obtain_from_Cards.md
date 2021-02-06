## 	[可获得的最大点数](https://leetcode-cn.com/problems/maximum-points-you-can-obtain-from-cards/)

一开始被标签的动态规划误导了，一直想的是和动规的博弈问题差不多

后来才想到滑动窗口，特别巧的一道题



### 代码实现

```go
func maxScore(cardPoints []int, k int) int {
	ans := 0
	n := len(cardPoints)
	for i := n - k; i < n; i++ {
		ans += cardPoints[i]
	}
	max := func(a, b int) int {
		if a > b {
			return a
		}
		return b
	}
	sum := ans
	for l, r := n-k, 0; l < n; r++ {
		sum = sum - cardPoints[l] + cardPoints[r]
		ans = max(ans, sum)
		l++
	}
	return ans
}
```

