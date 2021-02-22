## [根据字符出现频率排序](https://leetcode-cn.com/problems/sort-characters-by-frequency/)

用标准库实现了一遍堆(优先队列),要先定义一个类型实现堆规定的接口，才能使用标准库的堆操作函数

之前自己写过一个，比自己写性能高很多

### 代码实现

```go
func frequencySort(s string) string {
	S := []byte(s)
	ans := make([]byte, len(s))
	hash := make(map[byte]int)
	for _, v := range S {
		hash[v]++
	}
	pq := make(h, len(hash))
	i := 0
	for k, v := range hash {
		pq[i] = &Item{
			Value: k,
			Count: v,
		}
		i++
	}
	heap.Init(&pq)
	n := 0
	for pq.Len() > 0 {
		item := heap.Pop(&pq).(*Item)
		for i = 0; i < item.Count; i++ {
			ans[n] = item.Value
			n++
		}
	}
	return string(ans)
}

type Item struct {
	Value byte
	Count int
}
type h []*Item

func (pq h) Len() int {
	return len(pq)
}

func (pq h) Less(i, j int) bool {
	return pq[i].Count > pq[j].Count
}

func (pq h) Swap(i, j int) {
	pq[i], pq[j] = pq[j], pq[i]
}

func (pq *h) Push(x interface{}) {
	*pq = append(*pq, x.(*Item))
}

func (pq *h) Pop() interface{} {
	n := len(*pq) - 1
	item := (*pq)[n]
	(*pq)[n] = nil
	*pq = (*pq)[:n]
	return item
}
```

