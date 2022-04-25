# Stack
https://www.geeksforgeeks.org/stack-in-python/
https://lovedrinkcafe.com/python-stack-data-structure/
### 225. Implement Stack using Queues
#### 2022/04/20
```python=
class MyStack:
#第一種方法(better)
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.stack=[] #將data structure初始化的地方
        
    def push(self, x: int) -> None:
        """
        Push element x onto stack.
        """
        self.stack.append(x) #將element add到stack上
        
    def pop(self) -> int:
        """
        Removes the element on top of the stack and returns that element.
        """
        if self.stack:
            return self.stack.pop(-1) #將stack最上面的element移除，並return回去
        return None #stack為空list的情況
    
    def top(self) -> int:
        """
        Get the top element.
        """
        if self.stack:
            return self.stack[-1] #定義top是最後一個放進stack的element
        return None #stack為空list的情況

    def empty(self) -> bool:
        """
        Returns whether the stack is empty.
        """
        return self.stack==[] #判斷stack內部是否為空list

#第二種方法
#     def __init__(self):
#         """
#         Initialize your data structure here.
#         """
#         self._queue = collections.deque()

#     def push(self, x: int) -> None:
#         """
#         Push element x onto stack.
#         """
#         self._queue.append(x)
#         for _ in range(len(self._queue)-1):
#             self._queue.append(self._queue.popleft())
        

#     def pop(self) -> int:
#         """
#         Removes the element on top of the stack and returns that element.
#         """
#         return self._queue.popleft()
        

#     def top(self) -> int:
#         """
#         Get the top element.
#         """
#         return self._queue[0]
        

#     def empty(self) -> bool:
#         """
#         Returns whether the stack is empty.
#         """
#         return len(self._queue)==0 

# Your MyStack object will be instantiated and called as such:
# obj = MyStack()
# obj.push(x)
# param_2 = obj.pop()
# param_3 = obj.top()
# param_4 = obj.empty()
```

### 496. Next Greater Element I
#### 2022/04/23

我的解法:
```python=
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        lst=[]
        for i in nums1:
            if i in nums2:
                index = nums2.index(i)
                lst2=[]
                if index==len(nums2)-1:
                    lst.append("-1")
                else:
                    for j in range(index+1, len(nums2), 1):
                        if nums2[j] > i:
                            lst2.append(nums2[j])
                    if lst2:
                        lst.append(lst2[0])
                    else:
                        lst.append("-1")
            else:
                lst.append("-1")
                
        return lst
```

最佳解法:
```python=
def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
	if not nums2:
		return None

	mapping = {}
	result = []
	stack = []
	stack.append(nums2[0])

	for i in range(1, len(nums2)):
		while stack and nums2[i] > stack[-1]:       # if stack is not empty, then compare it's last element with nums2[i]
			mapping[stack[-1]] = nums2[i]           # if the new element is greater than stack's top element, then add this to dictionary 
			stack.pop()                             # since we found a pair for the top element, remove it.
		stack.append(nums2[i])                      # add the element nums2[i] to the stack because we need to find a number greater than this

	for element in stack:                           # if there are elements in the stack for which we didn't find a greater number, map them to -1
		mapping[element] = -1

	for i in range(len(nums1)):
		result.append(mapping[nums1[i]])
	return result
```