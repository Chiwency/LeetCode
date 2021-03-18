## [反转链表 II](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

更改指针，用一次遍历完成



### 代码实现

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseBetween(head *ListNode, left int, right int) *ListNode {
	pre, h := head, head
	l := pre
	for i := 0; i < left-2; i++ {
		pre = pre.Next
	}
	if left > 1 {
		h = pre.Next
		l = pre.Next
	}
	s := h.Next
	for i := 0; i < right-left; i++ {
		h.Next = s.Next
		s.Next = l
		l = s
		s = h.Next
	}
	if left > 1 {
		pre.Next = l
	} else {
		return l
	}
	return head
}

```

