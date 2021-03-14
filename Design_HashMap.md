## [设计哈希映射](https://leetcode-cn.com/problems/design-hashmap/)

和之前设计哈希表一样 取余，链表解决冲突





### 代码实现

```go
type item [2]int
type MyHashMap struct {
	dict [][]item
	size int
}

/** Initialize your data structure here. */
func Constructor() MyHashMap {
	dict := make([][]item, 10000)
	return MyHashMap{dict, 10000}
}

/** value will always be non-negative. */
func (this *MyHashMap) Put(key int, value int) {
	index := key % this.size
	new := item{key, value}
	flag := true
	for k, v := range this.dict[index] {
		if v[0] == key {
			this.dict[index][k] = new
			flag = false
			break
		}
	}
	if flag {
		this.dict[index] = append(this.dict[index], new)
	}
	return
}

/** Returns the value to which the specified key is mapped, or -1 if this map contains no mapping for the key */
func (this *MyHashMap) Get(key int) int {
	index := key % this.size
	ans := -1
	for _, v := range this.dict[index] {
		if v[0] == key {
			ans = v[1]
			break
		}
	}
	return ans
}

/** Removes the mapping of the specified value key if this map contains a mapping for the key */
func (this *MyHashMap) Remove(key int) {
	index := key % this.size
	top := len(this.dict[index]) - 1
	for k, v := range this.dict[index] {
		if v[0] == key {
			this.dict[index][k], this.dict[index][top] = this.dict[index][top], this.dict[index][k]
			this.dict[index] = this.dict[index][:top]
			break
		}
	}
	return
}

/**
 * Your MyHashMap object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Put(key,value);
 * param_2 := obj.Get(key);
 * obj.Remove(key);
 */
```

