## [公平的糖果棒交换](https://leetcode-cn.com/problems/fair-candy-swap/)

赶了下时间，用了最简单的思路解，感觉有点麻烦

再看下官方题解，啊，原来也是这尿性，，，，



### 代码实现

```go
func fairCandySwap(A []int, B []int) (ans []int) {
	mapA := make(map[int]bool)
	sumA := 0
	sumB := 0
	for _, v := range A {
		sumA += v
		mapA[v] = true
	}
	for _, v := range B {
		sumB += v
	}
	dif := (sumA - sumB) / 2
	for _, v := range B {
		if mapA[v+dif] {
			ans = []int{v + dif, v}
		}
	}
	return
}
```

