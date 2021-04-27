## [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

   一开始一直在想循环一遍的算法，后来还是用map循环两遍

看题解貌似也没有更优的解法了





### 代码实现

```go
func copyRandomList(head *Node) *Node {
	if head == nil {
		return nil
	}
	dict := make(map[*Node]*Node)
	p := head
	for p != nil {
		temp := &Node{
			p.Val,
			nil,
			nil,
		}
		dict[p] = temp
		p = p.Next
	}
	p = head
	for p != nil {
		dict[p].Next = dict[p.Next]
		dict[p].Random = dict[p.Random]
		p = p.Next
	}

	return dict[head]
}
```



