

## [等差子数组](https://leetcode-cn.com/problems/arithmetic-subarrays/)

主要注意函数传参，如果是切片，会改变切片底层数据的数据，所以不希望改变的话，要再copy一个切片去传值



### 代码实现

```go
func checkArithmeticSubarrays(nums []int, l []int, r []int) []bool {
	ans := make([]bool, len(l))
	for k, _ := range l {
		temp := make([]int, r[k]-l[k]+1)
		copy(temp, nums[l[k]:r[k]+1])
		ans[k] = isArithmetic(temp)
	}
	return ans
}

func isArithmetic(nums []int) bool {
	sort.Ints(nums)
	l := len(nums)
	if l == 1 {
		return true
	}
	dif := nums[1] - nums[0]
	for i := 1; i < l; i++ {
		if nums[i]-nums[i-1] != dif {
			return false
		}
	}
	return true
}
```

