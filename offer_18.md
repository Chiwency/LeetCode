## [剑指 Offer 18. 删除链表的节点 LCOF](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

简单题



### 代码实现

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteNode(head *ListNode, val int) *ListNode {
	if head == nil {
		return nil
	}
	p := head
	if p.Val == val {
		return p.Next
	}
	for p.Next != nil {
		if p.Next.Val == val {
			p.Next = p.Next.Next
			break
		}
		p = p.Next
	}
	return head
}
```

