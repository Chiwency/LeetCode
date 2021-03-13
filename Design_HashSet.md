## [设计哈希集合](https://leetcode-cn.com/problems/design-hashset/)

用链表解决冲突，开始用开放定址法会超时



### 代码实现

```go
type MyHashSet struct {
	hash [][]int
	size int
}

/** Initialize your data structure here. */
func Constructor() MyHashSet {
	hash := make([][]int, 4000)
	return MyHashSet{hash, 4000}
}

func (this *MyHashSet) Add(key int) {
	index := key % this.size
	if len(this.hash[index]) == 0 {
		this.hash[index] = []int{key}
	} else {
		this.hash[index] = append(this.hash[index], key)
	}
	return
}

func (this *MyHashSet) Remove(key int) {
	index := key % this.size
	l := len(this.hash[index])
	for i := 0; i < l; {
		if this.hash[index][i] == key {
			l--
			this.hash[index][i], this.hash[index][l] = this.hash[index][l], this.hash[index][i]
		} else {
			i++
		}
	}
	this.hash[index] = this.hash[index][:l]
	return
}

/** Returns true if this set contains the specified element */
func (this *MyHashSet) Contains(key int) bool {
	index := key % this.size
	for _, v := range this.hash[index] {
		if v == key {
			return true
		}
	}
	return false
}

/**
 * Your MyHashSet object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Add(key);
 * obj.Remove(key);
 * param_3 := obj.Contains(key);
 */
```

