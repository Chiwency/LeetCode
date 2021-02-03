## [滑动窗口中位数](https://leetcode-cn.com/problems/sliding-window-median/)

TMD 烦死了， 做了四个小时，，因为半路上看到用双堆写，搞了半天，真的无语，不难很繁

总是有一些奇奇怪怪的错误，有些点没考虑到



### 代码实现

```go
func medianSlidingWindow(nums []int, k int) (ans []float64) {
	if len(nums) == 0 {
		return
	}
	maxH := &MaxIntHeap{}
	minH := &MinIntHeap{}
	heap.Init(maxH)
	heap.Init(minH)
	temp := make([]int, k)
	copy(temp, nums[:k])
	sort.Ints(temp)
	for l, r := 0, k-1; l <= r; l++ {
		if l == r {
			heap.Push(maxH, temp[l])
			break
		}
		heap.Push(maxH, temp[l])
		heap.Push(minH, temp[r])
		r--
	}
	var mid float64
	if k%2 == 0 {
		mid = (float64((*minH)[0]) + float64((*maxH)[0])) / float64(2)
	} else {
		mid = float64((*maxH)[0])
	}
	ans = append(ans, mid)
	n := len(nums)
	for l, r := 0, k; r < n; r++ {
		if !maxH.Remove(nums[l]) {
			minH.Remove(nums[l])
		}
		l++
		if float64(nums[r]) <= mid {
			heap.Push(maxH, nums[r])
		} else {
			heap.Push(minH, nums[r])
		}

		if k%2 == 0 {
			for maxH.Len() < minH.Len() {
				heap.Push(maxH, heap.Pop(minH))
			}
			for maxH.Len() > minH.Len() {
				heap.Push(minH, heap.Pop(maxH))
			}
			mid = (float64((*minH)[0]) + float64((*maxH)[0])) / float64(2)
			ans = append(ans, mid)
		} else if k%2 == 1 {
			for minH.Len() >= maxH.Len() {
				heap.Push(maxH, heap.Pop(minH))
			}
			for maxH.Len()-minH.Len() > 1 {
				heap.Push(minH, heap.Pop(maxH))
			}
			mid = float64((*maxH)[0])
			ans = append(ans, mid)
		}
	}
	return
}

type MinIntHeap []int

func (h MinIntHeap) Len() int           { return len(h) }
func (h MinIntHeap) Less(i, j int) bool { return h[i] < h[j] }
func (h MinIntHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *MinIntHeap) Push(x interface{}) {
	*h = append(*h, x.(int))
}

func (h *MinIntHeap) Pop() interface{} {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[0 : n-1]
	return x
}

func (h *MinIntHeap) Remove(v int) bool {
	l := h.Len()
	for i := 0; i < l; i++ {
		if (*h)[i] == v {
			heap.Remove(h, i)
			return true
		}
	}
	return false
}

type MaxIntHeap []int

func (h MaxIntHeap) Len() int           { return len(h) }
func (h MaxIntHeap) Less(i, j int) bool { return h[i] > h[j] }
func (h MaxIntHeap) Swap(i, j int)      { h[i], h[j] = h[j], h[i] }

func (h *MaxIntHeap) Push(x interface{}) {
	*h = append(*h, x.(int))
}

func (h *MaxIntHeap) Pop() interface{} {
	old := *h
	n := len(old)
	x := old[n-1]
	*h = old[0 : n-1]
	return x
}

func (h *MaxIntHeap) Remove(v int) bool {
	l := len(*h)
	for i := 0; i < l; i++ {
		if (*h)[i] == v {
			heap.Remove(h, i)
			return true
		}
	}
	return false
}
```



