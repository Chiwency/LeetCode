## [乘积最大子数组](https://leetcode-cn.com/problems/maximum-product-subarray/)

又是一道动态规划题，首先确定dp数组和状态转移方程

设``dp[i]`` 表示{nums[0]....nums[i]}的乘积最大子数组的乘积

但是因为有正负区分，所以我们维护``dpMax``和``dpMin`` 两个数组,以应付正负数

状态转移方程为

```go
dpMax[i]=max(dpMax[i-1]*nums[i],dpMin[i-1]*nums[i],nums[i])
dpMin[i]=min(dpMax[i-1]*nums[i],dpMin[i-1]*nums[i],nums[i])
```

### 代码实现

```go

func maxProduct(nums []int) int {
	l := len(nums)
	dpMax := make([]int, l)
	dpMin := make([]int, l)
	dpMax[0] = nums[0]
	dpMin[0] = nums[0]
	result := nums[0]
	max := func(a, b, c int) int {
		if a >= b && a >= c {
			return a
		} else if b >= a && b >= c {
			return b
		}
		return c
	}
	min := func(a, b, c int) int {
		if a <= b && a <= c {
			return a
		} else if b <= a && b <= c {
			return b
		}
		return c
	}
	for i := 1; i < l; i++ {
		dpMax[i] = max(dpMax[i-1]*nums[i], dpMin[i-1]*nums[i], nums[i])
		dpMin[i] = min(dpMax[i-1]*nums[i], dpMin[i-1]*nums[i], nums[i])
	}
	for i := 0; i < l; i++ {
		result = max(result, dpMax[i], -1000)
	}
	return result
}
```



**动态规划进度（3/N），受上题影响，找dp数组找到二维的去了，一般二维的就是O(n2)的复杂度了，还是没想到可以设置两个dp数组。多做多看多积累，找准dp数组和状态转移方程**