## [笨阶乘](https://leetcode-cn.com/problems/clumsy-factorial/)

O(1)的空间复杂度，还只打败33%玩家，，，，

要把 **减法看成加负数**  一开始没想明白这个问题写的挺烦，把减法分开讨论，淦

### 代码实现

```go
func clumsy(N int) int {
	stack := 0
	l := N
	for r := N - 1; r >= 1; r-- {
		switch (N - r) % 4 {
		case 1:
			l *= r
		case 2:
			l /= r
		case 3:
			stack += l + r
			l = 0
		case 0:
			l = -r
		}
	}
	return stack + l
}
```

