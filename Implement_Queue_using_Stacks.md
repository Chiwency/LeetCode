## [用栈实现队列](https://leetcode-cn.com/problems/implement-queue-using-stacks/)

用两个向两头开的队列实现，左右开弓  原理很简单，debug麻烦一点





### 代码实现

```go
type MyQueue struct {
    posStack []int
    revStack []int
    length int
}

/** Initialize your data structure here. */
func Constructor() MyQueue {
    return MyQueue{}
}

/** Push element x to the back of queue. */
func (this *MyQueue) Push(x int)  {
    this.posStack=append(this.posStack,x)
    this.length++
}
 
func (this *MyQueue) ValidStack(){
    if len(this.revStack)==0{
        n:=len(this.posStack)-this.length
        temp:=make([]int,this.length)
        copy(temp,this.posStack[n:])
        for i:=this.length-1;i>=0;i--{
            this.revStack=append(this.revStack,temp[i])
            temp=temp[:i]
        }
    }
}

/** Removes the element from in front of queue and returns that element. */
func (this *MyQueue) Pop() int {
    this.ValidStack()
    l:=len(this.revStack)
    ans:=this.revStack[l-1]
    this.revStack=this.revStack[:l-1]
    this.length--
    return ans
}


/** Get the front element. */
func (this *MyQueue) Peek() int {
    this.ValidStack()
    top:=len(this.revStack)-1
    return this.revStack[top]
}


/** Returns whether the queue is empty. */
func (this *MyQueue) Empty() bool {
    return this.length==0
}


/**
 * Your MyQueue object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(x);
 * param_2 := obj.Pop();
 * param_3 := obj.Peek();
 * param_4 := obj.Empty();
 */
```

