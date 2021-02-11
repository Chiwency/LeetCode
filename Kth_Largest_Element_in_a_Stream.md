## [数据流中的第 K 大元素](https://leetcode-cn.com/problems/kth-largest-element-in-a-stream/)

每次要找到第K大的数，就只储存排序后的前K个数，每次插入一个就淘汰一个

一开始想的是每次都弹出N次，淦，超时了，头脑太简单



### 代码实现

```go
type KthLargest struct {
	k int
	h *IntHeap
}

func Constructor(k int, nums []int) KthLargest {
	h := make(IntHeap, len(nums))
	copy(h, nums)
	heap.Init(&h)
	return KthLargest{k, &h}
}

func (this *KthLargest) Add(val int) int {
	heap.Push(this.h, val)
	for this.h.Len() > this.k {
		heap.Pop(this.h)
	}
	return (*this.h)[0]
}

type IntHeap []int

func (h IntHeap) Len() int           { return len(h) }
func (h IntHeap) Less(i, j int) bool { return h[i] < h[j] }
func (h IntHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *IntHeap) Push(x interface{}) {
	*h = append(*h, x.(int))
}

func (h *IntHeap) Pop() interface{} {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[0 : n-1]
	return x
}

/**
 * Your KthLargest object will be instantiated and called as such:
 * obj := Constructor(k, nums);
 * param_1 := obj.Add(val);
 */
```

