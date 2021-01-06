## [驼峰式匹配](https://leetcode-cn.com/problems/camelcase-matching/)

  把每个query与pattern匹配，query与pattern每匹配一个字符就前移，如果不匹配，query是小写字符的话就放过，query前移，如果是大写字母的话就结束，匹配不上。具体看代码注释

### 代码实现

```go
func camelMatch(queries []string, pattern string) []bool {
	result := make([]bool, len(queries))
	patternByte := []byte(pattern)
	l := len(pattern)
	for k, query := range queries {
		queryByte := []byte(query)
		i := 0
		flag := true
		for _, letter := range queryByte {
			if i < l && letter == patternByte[i] {
				i++
				continue
			}
			// 如果是小写就放过,是大写就置false
			if letter >= 'A' && letter <= 'Z' {
				flag = false
				break
			}
		}
		// 只有pattern都被匹配完了而且不再出现大写字母才可
		if flag && i == l {
			result[k] = true
		}
	}
	return result
}
```



