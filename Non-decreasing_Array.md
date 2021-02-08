## [非递减数列](https://leetcode-cn.com/problems/non-decreasing-array/)

一道数组的简单题



### 代码实现

```go
func checkPossibility(nums []int) bool {
	prev := -1 << 63
	l := len(nums)
	flag := 0
	for i := 1; i < l; i++ {
		if nums[i] >= nums[i-1] {
			continue
		}
		if i > 1 {
			prev = nums[i-2]
		}
		if flag == 0 {
			if nums[i] >= prev {
				nums[i-1] = prev
			} else {
				nums[i] = nums[i-1]
			}
			flag++
			continue
		}
		return false
	}
	return true
}
```

