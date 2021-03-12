## [验证二叉树的前序序列化](https://leetcode-cn.com/problems/verify-preorder-serialization-of-a-binary-tree/)

一看题目就想出了题解，但是写起来太坑了，挂了好几次，有很多边界条件需要考虑



### 代码实现

```go
func isValidSerialization(preorder string) bool {
	b := strings.Split(preorder, ",")
	stack := 0
	l := len(b)
	for i := 0; i < l; {
		if b[i] != "#" {
			i++
			stack++
			continue
		}
		if stack < 0 {
			return false
		} else if stack == 0 {
			return i == l-1
		}
		for stack > 0 {
			i++
			stack--
			if i >= l {
				return false
			} else if b[i] != "#" {
				break
			}
		}
	}

	return stack == 0
}
```

