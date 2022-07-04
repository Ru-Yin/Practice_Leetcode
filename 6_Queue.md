# Queue

### 621. Task Scheduler
#### 2022/04/25

```python=
class Solution:
    def leastInterval(self, tasks: List[str], n: int) -> int:
        ##解題思路: 給定一個任務列表，任務和任務之間要有n個間隔，所以先找出出現次數最多的任務。把它安插在每個任務組別的最前面>>例如: tasks=[A, A, A, B, B], n=2，則會如下安排
#       [A, B, _,
#       A, B, _,
#       A]
#故計算最少任務總數的算式就會是 (k-1)*(n+1)+(出現最多次數的任務共有幾個) = (3-1)*(2+1)+1
# k=排列好的組別數，n+1=間隔數+安插在最前面的那個A
        ct = Counter(tasks) #先計算每個任務的出現次數
        maxx = max(ct.values()) #找出最大出現次數為多少
        nmax = len([v for v in ct.values() if v == maxx]) #用for loop一一尋找出現最大次數的任務是誰，並計算有幾個任務出現最大次數
        return max(len(tasks), (maxx - 1) * (n + 1) + nmax) #len(tasks)為n=0的情況下
```
### 232. Implement Queue using Stacks
#### 2022/04/27
```python=
class MyQueue:
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.stack=[] #將data structure初始化的地方

    def push(self, x: int) -> None:
        self.stack.append(x) #跟stack的放法一樣, 將element add到queue上
        
    def pop(self) -> int:
        if self.stack:
            return self.stack.pop(0) #因為這裡依循first in first out (FIFO), 所以第一個放進去的element，也會第一個被pop出來
        return None

    def peek(self) -> int:
        if self.stack:
            return self.stack[0] #依循first in first out (FIFO), 第一個被push的element也是queue最前頭那個
        return None
        
    def empty(self) -> bool:
        return self.stack==[]
        


# Your MyQueue object will be instantiated and called as such:
# obj = MyQueue()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.peek()
# param_4 = obj.empty()
```
