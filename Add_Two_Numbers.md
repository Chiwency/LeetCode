## [两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

和225周赛中等题类似，这次换了一种判断套路`l1 != nil || l2 != nil || carry != 0 `, 更简洁一点



### 代码实现

```go
func addTwoNumbers(l1 *ListNode, l2 *ListNode) (ans *ListNode) {
	carry := 0
	var p *ListNode
	for l1 != nil || l2 != nil || carry != 0 {
		node := new(ListNode)
		if ans == nil {
			ans = node
			p = node
		} else {
			p.Next = node
			p = node
		}
		a, b := 0, 0
		if l1 != nil {
			a = l1.Val
			l1 = l1.Next
		}
		if l2 != nil {
			b = l2.Val
			l2 = l2.Next
		}
		node.Val = (a + b + carry) % 10
		carry = (a + b + carry) / 10
	}
	return ans
}
```

