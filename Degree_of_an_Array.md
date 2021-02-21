## [数组的度](https://leetcode-cn.com/problems/degree-of-an-array/)

爬个坑，数组和切片不一样，数组复制是值复制，不会直接修改原数组内存  不像切片一样是指针



### 代码实现

```go
func findShortestSubArray(nums []int) int {
	hash := make(map[int][3]int)
	for k, v := range nums {
		if arr, ok := hash[v]; !ok {
			info := [3]int{1, k, k}
			hash[v] = info
		} else {
			arr[0]++
			arr[2] = k
			hash[v] = arr
		}
	}
	degree := 0
	ans := 0
	for _, v := range hash {
		if v[0] > degree {
			degree = v[0]
			ans = v[2] - v[1] + 1
		} else if v[0] == degree {
			ans = min(ans, v[2]-v[1]+1)
		}
	}
	return ans
}

func min(a, b int) int {
	if a < b {
		return a
	}
	return b
}
```

