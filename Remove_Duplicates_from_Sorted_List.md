## [删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)

是昨天每日一题的简化版本，原理一样

### 代码实现

```go
func deleteDuplicates(head *ListNode) *ListNode {
	prev := &ListNode{101, head}
	post := prev
	p := head
	for p != nil {
		if p.Val == prev.Val {
			prev.Next = p.Next
		} else {
			prev = prev.Next
		}
		p = p.Next
	}
	return post.Next
}
```

