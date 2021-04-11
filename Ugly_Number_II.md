## [丑数 II](https://leetcode-cn.com/problems/ugly-number-ii/)

写的时候一直想实现O(n)的时间复杂度，虽然写的理论上是，但是用了递归调用，后面提交的时候时间还是有点慢。

看题解还是动规好点，但也不像是典型的动规，只是用三个指针记录了每个数是否*2 *3 *5 挺巧妙的。





### 代码实现

```go
func nthUglyNumber(n int) int {
	arr := []int{1}
	p := 0
	for len(arr) < n {
		product := arr[p] * 2
		if product > arr[len(arr)-1] {
			arr = append(arr, product)
		}
		product = arr[p] * 3
		if product > arr[len(arr)-1] {
			arr = findNext(arr, p, product)
			arr = append(arr, product)
		}
		product = arr[p] * 5
		if product > arr[len(arr)-1] {
			arr = findNext(arr, p, product)
			arr = append(arr, product)
		}
		p++
	}
	return arr[n-1]
}

func findNext(arr []int, p, max int) []int {
	product := arr[p+1] * 2
	if product >= max {
		return arr
	}
	if product > arr[len(arr)-1] {
		arr = append(arr, product)
	}
	product = arr[p+1] * 3
	if product < max {
		arr = findNext(arr, p+1, product)
		if product > arr[len(arr)-1] {
			arr = append(arr, product)
		}
	}
	arr = findNext(arr, p+1, max)
	return arr
}
```

