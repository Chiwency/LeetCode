## [去除重复字母](https://leetcode-cn.com/problems/remove-duplicate-letters/)

要想到用栈，没想到的孩子太难了，，，，这种题还是要见多识广，熟做力扣

还是道贪心题，贪心策略是尽量让更小的字母在前面

### 代码实现

```go
func removeDuplicateLetters(s string) string {
	S := []byte(s)
	l := len(s)
	left := [26]int{}
	posess := [26]bool{}
	stack := make([]byte, 0)
	for _, v := range S {
		left[v-'a']++
	}
	for i := 0; i < l; i++ {
		for len(stack) != 0 {
			top := len(stack) - 1
			// 如果大于等于后一个字符且后面还有相同字符，就出栈
			if posess[S[i]-'a'] {
				left[S[i]-'a']--
				break
			} else if stack[top] >= S[i] && left[stack[top]-'a'] > 0 {
				posess[stack[top]-'a'] = false
				stack = stack[:top]

			} else {
				stack = append(stack, S[i])
				posess[S[i]-'a'] = true
				left[S[i]-'a']--
				break
			}
		}
		if len(stack) == 0 {
			stack = append(stack, S[i])
			posess[S[i]-'a'] = true
			left[S[i]-'a']--
		}
	}
	return string(stack)
}
```



