## [剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

用二分查找，最好别遍历



### 代码实现

```go
func search(nums []int, target int) int {
	ans := 0
	for l, r := 0, len(nums)-1; l <= r; {
		mid := (l + r) / 2
		if nums[mid] == target {
			ans++
			for i := mid + 1; i <= r; i++ {
				if nums[i] == target {
					ans++
				} else {
					break
				}
			}
			for i := mid - 1; i >= l; i-- {
				if nums[i] == target {
					ans++
				} else {
					break
				}
			}
			break
		} else if nums[mid] > target {
			r = mid - 1
		} else {
			l = mid + 1
		}
	}
	return ans
}
```

