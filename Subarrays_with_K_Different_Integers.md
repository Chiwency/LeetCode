## [K 个不同整数的子数组](https://leetcode-cn.com/problems/subarrays-with-k-different-integers/)

摸了几次坑，但是还是一遍过，双指针做感觉不是很难



### 代码实现

```go
func subarraysWithKDistinct(A []int, K int) int {
	hash := make(map[int]int)
	ans := 0
	n := len(A)
	for l, r := 0, 0; r < n; r++ {
		hash[A[r]]++
		kind := len(hash)
		if kind < K {
			continue
		} else if kind >= K {
			ans++
		}
		for kind > K {
			hash[A[l]]--
			if hash[A[l]] == 0 {
				delete(hash, A[l])
				kind--
			}
			l++
		}
		i := l
		visit := make(map[int]int)
		for hash[A[i]] > visit[A[i]]+1 {
			visit[A[i]]++
			ans++
			i++
		}
	}
	return ans
}
```

