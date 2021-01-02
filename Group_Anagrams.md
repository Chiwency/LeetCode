## [字母异位词分组](https://leetcode-cn.com/problems/group-anagrams/)

一开始想到用排序，但是感觉每个单词都排序时间复杂度会很高，然后自己用哈希表写了个原始的，结果还给我超时？？？？ 这不比排序好嘛。。。。好吧，可能是排序在n小的时候时间损耗几乎不计。

**注意使用切片排序`sort.Slice` , 不止一次见到过了。**

**还有头一次知道`map`也能求长。。。**

### 代码实现

```go
func groupAnagrams(strs []string) [][]string {
	dict := make(map[string][]string)
	for _, v := range strs {
		str := []byte(v)
        // 切片排序，要会用
		sort.Slice(str, func(i, j int) bool { return str[i] < str[j] })
		sortedStr := string(str)
		dict[sortedStr] = append(dict[sortedStr], v)
	}
	// 头一次知道len还能对map求长
	result := make([][]string, 0, len(dict))
	for _, v := range dict {
		result = append(result, v)
	}
	return result
}
```

