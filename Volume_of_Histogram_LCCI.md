## [直方图的水量](https://leetcode-cn.com/problems/volume-of-histogram-lcci/) 

一开始想的就是用栈解，但是调了好久， 对于这种步骤多思考细节，

**talk is cheap, show me the code** 经常看到这句话，如果说这道面试题要讲的话，拿到题我就能讲出用栈的思路，很简单，但是真正编码的时候就会碰到各种各样的问题，还有很多边界条件需要考虑，所以还是要多动手，多多coding。



### 代码实现

```go
func trap(height []int) int {
	stack := make([]int, 0)
	ans := 0
	for k, v := range height {
		top := len(stack) - 1
		if top < 0 {
			stack = append(stack, k)
			continue
		} else if v < height[stack[top]] {
			stack = append(stack, k)
			continue
		}
		level := 0 // 水位
		for top >= 0 {
			if height[stack[top]] > v {
				ans += (v - level) * (k - stack[top] - 1)
				break
			}
			ans += (height[stack[top]] - level) * (k - stack[top] - 1)
			level = height[stack[top]]
			top--
		}
		top++
		stack = stack[:top]
		stack = append(stack, k)
	}
	return ans
}

```



