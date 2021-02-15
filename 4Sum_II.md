## [四数相加 II](https://leetcode-cn.com/problems/4sum-ii/)

分组思想，A/B一组，C/D一组

瞄了一眼题解，看到分组哈希的标题就想到了这么写，分组可以降低时间复杂度，很好的思想，以后要注意



### 代码实现

```go
func fourSumCount(A []int, B []int, C []int, D []int) int {
	aMap := make(map[int]int)
	ans := 0
	for _, v1 := range A {
		for _, v2 := range B {
			aMap[v1+v2]++
		}
	}
	for _, v1 := range C {
		for _, v2 := range D {
			ans += aMap[-v1-v2]
		}
	}

	return ans
}
```

