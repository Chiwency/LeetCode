## [扁平化嵌套列表迭代器](https://leetcode-cn.com/problems/flatten-nested-list-iterator/)

瞄下题解才发现能用dfs写， 没想到dfs的时候写的好复杂

还是要努力练成不看标签就知道解法的能力

之前能秒中等题还是太依赖看标签了

怪不得周赛老打不好



### 代码实现

```go
type NestedIterator struct {
	arry []int
	p    int
}

func Constructor(nestedList []*NestedInteger) *NestedIterator {
	arry := make([]int, 0)
	var dfs func(nestedList []*NestedInteger)
	dfs = func(nestedList []*NestedInteger) {
		for _, v := range nestedList {
			if v.IsInteger() {
				arry = append(arry, v.GetInteger())
			} else {
				dfs(v.GetList())
			}
		}
		return
	}
	dfs(nestedList)
	return &NestedIterator{arry, 0}
}

func (this *NestedIterator) Next() int {
	this.p++
	return this.arry[this.p-1]
}

func (this *NestedIterator) HasNext() bool {
	return this.p < len(this.arry)
}
```

