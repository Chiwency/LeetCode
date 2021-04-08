## [寻找旋转排序数组中的最小值](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array/)

自行设计二分查找方法，时间复杂度和二分差不多，只是多了个判断条件



### 代码实现

```go
func findMin(nums []int) int {
	l, r := 0, len(nums)-1
	ans := nums[r]
	var mid int
	for l <= r {
		mid = (l + r) / 2
		if nums[mid] < nums[len(nums)-1] {
			ans = nums[mid]
			r = mid - 1
		} else {
			l = mid + 1
		}
	}
	return ans
}
```

