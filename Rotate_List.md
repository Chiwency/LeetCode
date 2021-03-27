## [旋转链表](https://leetcode-cn.com/problems/rotate-list/)

看题解是先把链表连接成环，然后从指定位置断开就可，我没注意到这个规律，只能一次次迭代移动，为了储存所有的前驱节点还用了数组，时间复杂度O(n),淦！





### 代码实现

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func rotateRight(head *ListNode, k int) *ListNode {
	if head == nil || head.Next == nil {
		return head
	}
	nodes := []*ListNode{head}
	p := head.Next
	n := 1
	for p != nil {
		nodes = append(nodes, p)
		n++
		p = p.Next
	}
	k = k % n
	top := len(nodes) - 1
	for i := 0; i < k; i++ {
		nodes[top].Next = head
		head = nodes[top]
		nodes[top-1].Next = nil
		top--
	}
	return head
}
```

