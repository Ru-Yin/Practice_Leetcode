# Linked list (Class & OOPS)
https://itcosmos.co/python-oop-class/?fbclid=IwAR1HIdhYTHU1iygBXQhC2QJ1q-e3CG1P_P4Aw0oCqgOuu77z2ioqOTX2jf0
http://alrightchiu.github.io/SecondRound/linked-list-introjian-jie.html?fbclid=IwAR2r1NdrINgnCSQQi1z1N60EYhibHGamucic4Tx8BmuBGFmAXCvU76vHeTA
file:///C:/Users/Ring/Downloads/Introducing-Python-2%20(4).pdf
### 206. Reverse Linked List
#### 2022/04/01
```python=
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def reverseList(self, head: Optional[ListNode]) -> Optional[ListNode]:
        prev = None
        while head:
            next = head.next
            head.next = prev ##重新定義下一個element其實是指標的前一個
            prev = head
            head = next
        return prev
```
### 141. Linked List Cycle
#### 2022/04/11
```python=
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def hasCycle(self, head: Optional[ListNode]) -> bool:
        seen = set() ##紀錄已看過element的set list (遍歷列表)
        current = head ##顯示當前object
        while current: ##從list依序檢視每個element
            if current in seen:  ##若存在cycle，則current會存在在遍歷列表
                return True
            else:
                seen.add(current) ##若還沒遇到cycle，則會繼續下去
                current = current.next ##找下一個object
        return False ##沒有cycle表示前者的條件式不會return True，所以就return False
```
### 203. Remove Linked List Elements
#### 2022/4/14
```python=
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def removeElements(self, head: Optional[ListNode], val: int) -> Optional[ListNode]:
        while head != None and head.val == val: 
#保證linked list的第一個節點的值不等於val
            head=head.next
        if head==None: ##判斷linked list是否為空list
            return None
        headNode = head ##頭節點
        while head.next != None:
            if head.next.val==val:
                head.next=head.next.next
 ##跳過指定值並指認指定值的下一個值為當前的下一個
            else:
                head=head.next ##其他正常指標
        return headNode
```
### 234. Palindrome Linked List
#### 2022/4/17
```python=
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def isPalindrome(self, head: Optional[ListNode]) -> bool:
        fast=slow=head #剛開始設定兩個stride (slow and fast)，並於同一起始點(head)開始走
        stak=[] #紀錄slow走過的node用的list
        while fast and fast.next: #當fast和fast.next走到null之前
            stak.append(slow.val) #stak開始記錄slow走過的node
            slow=slow.next #slow為正常走(next步伐為1)
            fast=fast.next.next #fast為一次走兩步(next步伐為2)
            #由於fast的速率為slow的兩倍，所以當fast走到null時，slow會停在linked list的中點
        if fast: #此情況用於linked list的node為奇數時
            slow=slow.next #中點要再加一
        while slow:
            top=stak.pop() #將stak從尾至頭拿出 (==從List的中點至起點依序拿出)
            if top != slow.val: #看stak拿出的node值是否等於中點在往下走的node值 ([top<<<<中點>>>>slow.val])
                return False #若不等於則false
            slow=slow.next #slow從中點往下(右)走
        return True
```
### 237. Delete Node in a Linked List
#### 2022/4/18
https://www.geeksforgeeks.org/linked-list-set-3-deleting-node/
```python=
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution:
    def deleteNode(self, node):
        """
        :type node: ListNode
        :rtype: void Do not return anything, modify node in-place instead.
        """
        if node: #若當前位置為node
            node.val=node.next.val #則將當前位置的值取代為其下一個node的值
            node.next=node.next.next #則將當前位置的node取代為其下一個node
        else:
            return node #其他node正常輸出
```
