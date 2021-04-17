##  [剑指 Offer 58 - I. 翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

用栈从右往左读，还是较简单



### 代码实现

```go
func reverseWords(s string) string {
	s = " " + s
	arr := []byte(s)
	stack := make([]byte, 0)
	ans := ""
	for i := len(arr) - 1; i >= 0; i-- {
		if arr[i] == ' ' && len(stack) > 0 {
			ans += " "
			for j := len(stack) - 1; j >= 0; j-- {
				ans += string(stack[j])
			}
			stack = stack[:0]
		} else if arr[i] != ' ' {
			stack = append(stack, arr[i])
		}
	}
	if ans == "" {
		return ans
	}
	return ans[1:]
}

```

