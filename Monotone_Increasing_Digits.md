## [单调递增的数字](https://leetcode-cn.com/problems/monotone-increasing-digits/)

贪心算法

切分数字还可以用`s := []byte(strconv.Itoa(n))` 更简洁

### 代码实现

```go
func monotoneIncreasingDigits(N int) int {
	nums := make([]int, 0)
	for N > 0 {
		nums = append(nums, N%10)
		N /= 10
	}
	l := len(nums)
	n := l
	flag := false
	for i := l - 1; i >= 1; i-- {
		if flag {
			nums[i] = 9
			continue
		}
		if nums[i] > nums[i-1] {
			n = i
			nums[i] -= 1
			nums[i-1] = 9
			nums[0] = 9
			flag = true
		}
	}
	for i := n; i < l-1; i++ {
		if nums[i] < nums[i+1] {
			nums[i] = 9
			nums[i+1] -= 1
		} else {
			break
		}
	}
	ans := 0
	for i := l - 1; i >= 0; i-- {
		ans = nums[i] + ans*10
	}

	return ans
}
```

