### [寻找数组的中心索引](https://leetcode-cn.com/problems/find-pivot-index/)

本来想能不能一次遍历就解出来的，用双指针左右开弓，哪边的和小哪边前进一位，但是忽略了负数的情况

`1 2 3 4 5 6` 和 `-1 -1 -1 -1 0` ，两种情况不能一概而论，所以测到三百多用例的时候挂掉了，，，



### 代码实现

```go
func pivotIndex(nums []int) int {
	sum := 0
	for _, v := range nums {
		sum += v
	}
	left := 0
	for k, v := range nums {
		if 2*left == sum-v {
			return k
		}
		left += v
	}
	return -1
}
```

