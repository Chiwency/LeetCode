## [ 基本计算器 II](https://leetcode-cn.com/problems/basic-calculator-ii/)

也是转化成后缀表达式再计算 代码有点繁，需要注意很多细节



### 代码实现

```go
func calculate(s string) int {
	s1 := []int{}
	s2 := []byte{}
	s = strings.ReplaceAll(s, " ", "")
	S := []byte(s)
	ops := map[byte]int{'+': 0, '-': 0, '*': 1, '/': 1}
	for i := 0; i < len(S); {
		if S[i] >= '0' && S[i] <= '9' {
			num := 0
			for i < len(S) && S[i] >= '0' && S[i] <= '9' {
				num = num*10 + int(S[i]-'0')
				i++
			}
			s1 = append(s1, num)
		} else {
			top := len(s2) - 1
			if top < 0 || ops[S[i]] > ops[s2[top]] {
				s2 = append(s2, S[i])
			} else {
				n := len(s1) - 1
				for top >= 0 && ops[S[i]] <= ops[s2[top]] {
					switch s2[top] {
					case '+':
						s1[n-1] = s1[n] + s1[n-1]
					case '-':
						s1[n-1] = s1[n-1] - s1[n]
					case '*':
						s1[n-1] = s1[n-1] * s1[n]
					case '/':
						s1[n-1] = s1[n-1] / s1[n]
					}
					s1 = s1[:n]
					n--
					s2 = s2[:top]
					top--
				}
				s2 = append(s2, S[i])
			}
			i++
		}
	}

	for top, n := len(s2)-1, len(s1)-1; top >= 0; {
		switch s2[top] {
		case '+':
			s1[n-1] = s1[n] + s1[n-1]
		case '-':
			s1[n-1] = s1[n-1] - s1[n]
		case '*':
			s1[n-1] = s1[n-1] * s1[n]
		case '/':
			s1[n-1] = s1[n-1] / s1[n]
		}
		s1 = s1[:n]
		n--
		s2 = s2[:top]
		top--
	}
	return s1[0]
}
```

