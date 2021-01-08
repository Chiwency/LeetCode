## [优势洗牌](https://leetcode-cn.com/problems/advantage-shuffle/)

看完题目就想到了田忌赛马，用最微弱的优势取胜对手，尽肯能拿到更多的胜利

所以要先排序，挺简单的



### 代码实现

```go
func advantageCount(A []int, B []int) []int {
	sort.Ints(A)
	l := len(B)
	n := len(A)
	result := make([]int, n)
	// 储存result中没有填上元素的位置
	queue := make([]int, 0)
	for i := 0; i < l; i++ {
		j := 0
		for ; j < n; j++ {
			if A[j] > B[i] {
				result[i] = A[j]
				A[j] = -1
				break
			}
		}
		if j == n {
			queue = append(queue, i)
		}
	}

	for i := 0; i < n; i++ {
		if A[i] != -1 {
			index := queue[0]
			queue = queue[1:]
			result[index] = A[i]
		}
	}
	return result
}
```

