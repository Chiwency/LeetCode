## [下一个更大元素 II](https://leetcode-cn.com/problems/next-greater-element-ii/)

一般涉及数组的题要想下能不能用栈或队列做  要不是按`tag`来做题，一开始不会想到用栈，可能会用嵌套循环，时间复杂度就到了O(n2), 用栈的话复杂度就降到了O(n)



> 不过看题解写的比较简洁优雅，我这种没有设置条件的循环很有可能会导致无限循环 以后尽量少用

### 代码实现

```go
func nextGreaterElements(nums []int) []int {
	l := len(nums)
	stack := make([]int, 0)
	result := make([]int, l)
	if l == 0 {
		return result
	}
	i := 0
	for {
		n := i % l
		top := len(stack) - 1
		// 已经确定的跳过
		if top < 0 {
			stack = append(stack, n)
			i++
			continue
		}
		// 如果遍历了一圈又回到了栈底位置，就清空栈
		if i > n && n == stack[0] {
			result[stack[0]] = -1
			for j := 1; j <= top; j++ {
				if nums[stack[j]] < nums[stack[0]] {
					result[stack[j]] = nums[stack[0]]
				} else {
					result[stack[j]] = -1
				}
			}
			break
		}
		// 如果遇到更大的，就出栈，并记录这个更大值
		if nums[stack[top]] < nums[n] {
			result[stack[top]] = nums[n]
			stack = stack[:top]
		} else if i >= l { // 第二遍循环的话就不用再入栈了
			i++
		} else {
			i++
			stack = append(stack, n)
		}
	}

	return result
}
```

