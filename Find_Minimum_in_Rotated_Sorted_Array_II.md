## [寻找旋转排序数组中的最小值 II](https://leetcode-cn.com/problems/find-minimum-in-rotated-sorted-array-ii/)

和昨天每日一题一样，只是多了重复的条件，左右两端去重即可，上一题我是直接递归，这次就学乖了，，，，而且上一题是查找target，去重的时候左右都去掉，我一开始直接效仿，错了好几次，，，因为这次是找最小值，最右边的值作为判断依据不能动，所以去重只能去左边。



### 代码实现

```go
func findMin(nums []int) int {
	ans := nums[len(nums)-1]
	l, r := 0, len(nums)-1
	for l <= r {
		if l != r && nums[l] == nums[r] {
			l++
			continue
		}
		mid := (l + r) / 2
		if nums[mid] <= nums[len(nums)-1] {
			ans = nums[mid]
			r = mid - 1
		} else {
			l = mid + 1
		}
	}
	return ans
}
```

