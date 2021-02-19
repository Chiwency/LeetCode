## [等差数列划分](https://leetcode-cn.com/problems/arithmetic-slices/)

假的动规，被误导了，直接按正常思路做就很简单



### 代码实现

```go
func numberOfArithmeticSlices(A []int) int {
	ans := 0
	l := len(A)
	count := 0
	if l < 3 {
		return 0
	}
	d := A[1] - A[0]
	for i := 2; i < l; i++ {
		if A[i]-A[i-1] == d {
			count++
			ans += count
		} else {
			d = A[i] - A[i-1]
			count = 0
		}
	}

	return ans
}
```

