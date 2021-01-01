## [自定义字符串排序](https://leetcode-cn.com/problems/custom-sort-string/)

用map做，问题还是一样的，有时候大意了，会忽略一些情况，这次又是挂了两次才提交成功。成功率惨淡。

有些字符串题看起来简单，但是很容易做错，不像动态规划有了思路基本就能一次过。

### 代码实现

```go
func customSortString(S string, T string) string {
	s := []byte(S)
	t := []byte(T)
	result := make([]byte, len(t))
	index := 0
	wordsDict := make(map[byte]int)
	for _, v := range t {
		_, exist := wordsDict[v]
		if exist {
			wordsDict[v]++
		} else {
			wordsDict[v] = 1
		}

	}
	for _, v := range s {
		_, exist := wordsDict[v]
		if exist {
			for i := 0; i < wordsDict[v]; i++ {
				result[index] = v
				index++
			}
			delete(wordsDict, v)
		}
	}
	for v := range wordsDict {
		for i := 0; i < wordsDict[v]; i++ {
			result[index] = v
			index++
		}
	}

	return string(result)
}
```



