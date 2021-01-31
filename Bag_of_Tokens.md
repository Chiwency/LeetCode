## [令牌放置](https://leetcode-cn.com/problems/bag-of-tokens/)

双指针＋排序，不是很难



### 代码实现

```go
func bagOfTokensScore(tokens []int, P int) int {
	sort.Ints(tokens)
	ans := 0
	l, r := 0, len(tokens)-1
	for l <= r {
		if tokens[l] <= P {
			P -= tokens[l]
			ans++
			l++
		} else if l != r && ans > 0 {
			ans--
			P += tokens[r]
			r--
		} else {
			break
		}
	}
	return ans
}
```

