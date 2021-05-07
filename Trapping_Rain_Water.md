## [接雨水](https://leetcode-cn.com/problems/trapping-rain-water/)

之前绝对写过这道题，但是不知道为什么没记录，在面经里面看到了又做一遍

之前写的时候有点繁，看了双指针的解法，然后这次就尝试用双指针，理清了逻辑就很简单



### 代码实现

```go
func trap(height []int) int {
	sum, own := 0, 0
	l, r := 0, len(height)-1
	level := 0
	for l < r {
		if height[l] >= height[r] {
			if height[r] <= level {
				own += height[r]
				r--
				continue
			}
			sum += (height[r] - level) * (r - l + 1)
			level = height[r]
			own += height[r]
			r--

		} else {
			if height[l] <= level {
				own += height[l]
				l++
				continue
			}
			sum += (height[l] - level) * (r - l + 1)
			level = height[l]
			own += height[l]
			l++
		}
	}
	return sum - own - level
}
```

