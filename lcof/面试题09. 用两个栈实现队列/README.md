# [面试题09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

## 题目描述
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 -1 )

**示例 1：**

```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```

**示例 2：**

```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```

**提示：**

- `1 <= values <= 10000`
- `最多会对 appendTail、deleteHead 进行 10000 次调用`

## 解法
### Python3
```python
class CQueue:

    def __init__(self):
        self._s1 = []
        self._s2 = []
    
    def _check(self):
        if not self._s2:
            while self._s1:
                self._s2.append(self._s1.pop())

    def appendTail(self, value: int) -> None:
        self._s1.append(value)
        self._check()

    def deleteHead(self) -> int:
        self._check()
        return -1 if not self._s2 else self._s2.pop()


# Your CQueue object will be instantiated and called as such:
# obj = CQueue()
# obj.appendTail(value)
# param_2 = obj.deleteHead()
```

### Java
```java
class CQueue {
    private Stack<Integer> s1 = new Stack<>();
    private Stack<Integer> s2 = new Stack<>();

    public CQueue() {

    }
    
    public void appendTail(int value) {
        s1.push(value);
        check();
    }
    
    public int deleteHead() {
        check();
        return s2.empty() ? -1 : s2.pop();
    }

    private void check() {
        if (s2.empty()) {
            while (!s1.empty()) {
                s2.push(s1.pop());
            }
        }
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```

### JavaScript
```js
var CQueue = function() {
    this.data = []
    this.helper = []
};
/** 
 * @param {number} value
 * @return {void}
 */
CQueue.prototype.appendTail = function(value) {
    this.data.push(value)
};
/**
 * @return {number}
 */
CQueue.prototype.deleteHead = function() {
    if(this.data.length) {
        while(this.data.length > 1) {
            this.helper.push(this.data.pop())
        }
        let res = this.data.pop()
        while(this.helper.length) {
            this.data.push(this.helper.pop())
        }
        return res
    } else {
        return -1
    }
};
```

### Go

```go
type CQueue struct {
    Stack1 []int
    Stack2 []int
}
// 入队都往S1压入，弹出时判定S2是否为空，S2非空则弹出S2顶
//否则，S1的元素从栈顶依次入S2,再从S2弹出

func Constructor() CQueue {
    return CQueue{Stack1:[]int{},Stack2:[]int{}}
}


func (this *CQueue) AppendTail(value int)  {
    this.Stack1 = append(this.Stack1, value)
}


func (this *CQueue) DeleteHead() int {
    if len(this.Stack1) == 0 && len(this.Stack2) == 0 {
        return -1
    }
    if len(this.Stack2) > 0 {
        res := this.Stack2[len(this.Stack2)-1]
        this.Stack2 = this.Stack2[0:len(this.Stack2)-1]
        return res
    }
    for len(this.Stack1) > 0 {
        this.Stack2 = append(this.Stack2,this.Stack1[len(this.Stack1)-1])
        this.Stack1 = this.Stack1[0:len(this.Stack1)-1]
    }
    res := this.Stack2[len(this.Stack2)-1]
    this.Stack2 = this.Stack2[0:len(this.Stack2)-1]
    return res
}
```



### ...

```

```
