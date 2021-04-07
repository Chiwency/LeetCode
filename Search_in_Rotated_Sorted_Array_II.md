## [搜索旋转排序数组 II](https://leetcode-cn.com/problems/search-in-rotated-sorted-array-ii/)

和官方题解差不多，但是碰到`1 0 1 1 1` 和`1 1 1 0 1`    这种情况时，无法判断mid是在左边还是在右边部分，所以碰到左右相等的情况， 我为了快点AC，直接用递归了，，，，，没想到可以自行跳过左右两边相等的情况  淦 所以空间复杂度有亿点点高 



### 代码实现

```go
func search(nums []int, target int) bool {
	if len(nums) < 1 {
		return false
	}
	l, r := 0, len(nums)-1
	for r >= l {
		mid := (l + r) / 2
		if nums[mid] == target || nums[l] == target || nums[r] == target {
			return true
		}
		if nums[l] == nums[r] {
			return search(nums[l:r], target)
		}
		if target > nums[0] {
			if nums[mid] > target || nums[mid] < nums[0] {
				r = mid - 1
			} else {
				l = mid + 1
			}
		} else {
			if nums[mid] < target || nums[mid] > nums[len(nums)-1] {
				l = mid + 1
			} else {
				r = mid - 1
			}
		}
	}
	return false
}
```

