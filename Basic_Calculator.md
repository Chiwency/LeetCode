## [基本计算器](https://leetcode-cn.com/problems/basic-calculator/)

好家伙，用双栈把它变成后缀表达式再计算，还要处理负数的问题，，，，及其复杂，加上debug弄了三个多小时。  但是原理比较简单，就是代码麻烦，有很多忽略的细节。

因为是只处理括号和加减法，没有优先级的问题，所以可以不用变成后缀表达式，官方题解写的更简单



### 代码实现

```go
func calculate(s string) int {
	s = strings.ReplaceAll(s, " ", "")
	s = strings.ReplaceAll(s, "(-", "(0-")
	if s[:1] == "-" {
		s = "0" + s
	}
	postExp := PostfixExpression(s)
	stack := make([]string, 0)
	for _, v := range postExp {
		k := len(stack)
		if v == "+" || v == "-" {
			num1, _ := strconv.Atoi(stack[k-2])
			num2, _ := strconv.Atoi(stack[k-1])
			if v == "-" {
				stack[k-2] = strconv.Itoa(num1 - num2)
			} else {
				stack[k-2] = strconv.Itoa(num2 + num1)
			}
			stack = stack[:k-1]
		} else {
			stack = append(stack, v)
		}
	}
	ans, _ := strconv.Atoi(stack[0])
	return ans
}

func PostfixExpression(s string) []string {
	S := []byte(s)
	s1 := make([]string, 0)
	s2 := make([]string, 0)
	operator := map[byte]bool{'+': true, '-': true, '(': true, ')': true}
	for i := 0; i < len(S); i++ {
		v := S[i]
		if operator[v] {
			if v == ' ' {
				continue
			}
			if v != ')' {
				top := len(s2) - 1
				if top >= 0 && s2[top] != "(" && v != '(' {
					s1 = append(s1, s2[top])
					s2 = s2[:top]
				}
				s2 = append(s2, string(v))
				continue
			}
			top := len(s2) - 1
			for s2[top] != "(" {
				s1 = append(s1, string(s2[top]))
				top--
			}
			s2 = s2[:top]
		} else if v >= '0' && v <= '9' {
			num := 0
			flag := false
			for i < len(S) && S[i] >= '0' && S[i] <= '9' {
				num = num*10 + int(S[i]-'0')
				i++
				flag = true
			}
			if flag {
				i--
			}
			s1 = append(s1, strconv.Itoa(num))
		}
	}
	top := len(s2) - 1
	for top >= 0 {
		s1 = append(s1, s2[top])
		top--
	}
	return s1
}
```

