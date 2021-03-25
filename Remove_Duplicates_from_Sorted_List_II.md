## [删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)

因为有可能从head开始就重复，有两种情况，分情况讨论显然比较麻烦，所以想到在head前面加上一个不可能重复的节点，就可以将两种情况统一，简化了代码。



### 代码实现

```go

/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func deleteDuplicates(head *ListNode) *ListNode {

	myHead := &ListNode{101, head}
	head = &ListNode{0, myHead}
	prev := myHead
	this := myHead.Next
	for this != nil {
		if this.Val == prev.Val {
			head.Next = this.Next
		} else if this != head.Next {
			head = head.Next
		}
		prev = this
		this = this.Next
	}
	return myHead.Next
}
```

