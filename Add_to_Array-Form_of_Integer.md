## [数组形式的整数加法](https://leetcode-cn.com/problems/add-to-array-form-of-integer/)

主要是考虑溢出，所以要从低到高逐位相加



### 代码实现

```go
func addToArrayForm(A []int, K int) []int {
	nums := make([]int, 0)
	for K > 0 {
		nums = append(nums, K%10)
		K /= 10
	}
	l := len(nums)
	for i := 0; i < l/2; i++ {
		nums[i], nums[l-i-1] = nums[l-i-1], nums[i]
	}
	base, add := A, nums
	if len(A) < l {
		base, add = nums, A
	}
	carry := 0
	for i, j := len(add)-1, len(base)-1; j >= 0; j-- {
		sum := base[j] + carry
		if i >= 0 {
			sum += add[i]
			i--
		}
		base[j] = sum % 10
		carry = sum / 10
	}
	if carry != 0 {
		ans := []int{carry}
		ans = append(ans, base...)
		return ans
	}

	return base
}
```

