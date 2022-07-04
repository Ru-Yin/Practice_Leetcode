# Graph-DFS
## 104. Maximum Depth of Binary Tree
#### 2022/5/29
參考來源: https://www.youtube.com/watch?v=hTM3phVI6YQ&ab_channel=NeetCode
目的: 找出 binary tree的最大高度
### solution-1: Recursive DFS
![](https://i.imgur.com/jGWDoFD.jpg)

1.以3為root
2. 比較左邊及右邊的tree的node數，選取最大node樹的一邊，並向下找其child node，直至找不到任何child node
3. 由於起初3為一個node所以+1
4. 再加上比較後，最大一邊的node數，即為答案

```python=
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if root==None: #若此root沒有child node則return 0
            return 0
        return 1+max(self.maxDepth(root.left), self.maxDepth(root.right)) 
        #1為最剛開始的root node，並加上左右兩邊tree最大值一方的node數
```

### solution-2: BFS
![](https://i.imgur.com/a5QYgh3.png)

```python=
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        if not root:
            return 0
        level = 0
        q = deque([root])
        while q:
            for i in range(len(q)):
                node = q.popleft()
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            level +=1
        return level
```
### solution-3: Iterative DFS
![](https://i.imgur.com/L3Hl3dO.png)
```python=
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def maxDepth(self, root: Optional[TreeNode]) -> int:
        stack = [[root, 1]]
        res = 0
        while stack:
            node, depth =stack.pop()
            if node:
                res = max(res, depth)
                stack.append([node.left, depth+1])
                stack.append([node.right, depth+1])
        return res
```

## 101. Symmetric Tree
#### 2022/5/31
參考來源: https://ithelp.ithome.com.tw/articles/10213277?sc=pt
目的: 判斷其是否為對稱的tree
```python=
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def isSymmetric(self, root: Optional[TreeNode]) -> bool:
        if not root:
            #當root走到末端時，其child 均為 null，回傳True
            return True
        #若root未走到tree末端，則需要透過function Sym判斷
        return self.Sym(root.left, root.right)
#另建一個function判斷root不為null時的情況，input為左子樹及右子樹
    def Sym(self, l: TreeNode, r: TreeNode) -> bool:
        if not l and not r:
            #若左子樹及右子樹均為null的情況 (對稱)
            return True
        if not l or not r:
            #若只有其中一個子樹為null的情況 (不對稱)
            return False
        #判斷以下條件並回傳布林值:
        # l.val==r.val 判斷第二層左子樹的值是否==第二層右子樹的值
        # self.Sym(l.left, r.right) 判斷左子樹的左側值是否==右子樹右側值
        # self.Sym(l.right, r.left) 判斷左子樹的右側值是否==右子樹左側值
        return l.val==r.val and self.Sym(l.left, r.right) and self.Sym(l.right, r.left)
        # 以上三條件均符合則回傳True, 否則回傳False
```
## 114. Flatten Binary Tree to Linked List
#### 2022/6/1
參考來源: 
* https://blog.csdn.net/fuxuemingzhu/article/details/70241424
* https://shubo.io/iterative-binary-tree-traversal/

目的: 將binary tree整理成一個linked list (左子樹均為null, 右子樹為排序過的linked list)
```python=
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def flatten(self, root: Optional[TreeNode]) -> None:
        """
        Do not return anything, modify root in-place instead.
        """
        res = []
        #建立此tree排序後的list
        self.preorder(root, res)
        
        #依照這個list，另外畫出一新tree (並取代原本的tree)
        for i in range(len(res)-1):
            res[i].left = None #左子樹一律均為none
            res[i].right = res[i+1] #右子樹由於要塞進原左子樹的node，所以均會順移一個位置，將自己原本的位置給原左子樹的node
    
    def preorder(self, root, res):
        if not root:
        #若tree為none時，回傳原tree
            return 
        #開一個空list，存儲排序後的node順序: root -> root.left -> root.right
        res.append(root)
        self.preorder(root.left, res)
        self.preorder(root.right, res)
```
## 105. Construct Binary Tree from Preorder and Inorder Traversal
#### 2022/6/3
參考來源: https://www.wongwonggoods.com/python/python_leetcode/leetcode-python-105/
目的: 透過input提供的inorder及preorder list，構出其相對應的linked list
```python=
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def buildTree(self, preorder: List[int], inorder: List[int]) -> Optional[TreeNode]:
        if not preorder or not inorder:
            return None #當前root走到底時，回傳null
        val = preorder[0] #最能確定當前root的方法，便是認出preorder的第一個位置
        root = TreeNode(val) #設定linked list 的 root
        idx = inorder.index(val) #找出root在inorder的位置
        #定義左子樹
        #以preorder來說，便是除了第一個位置(root的位置)以後，到左子樹總node數(總node數可從inoder的root index看出，即root index左側均為左子樹node)的位置均為左子樹範疇
        #以inorder來說，root index之前的位置均屬左子樹
        root.left = self.buildTree(preorder[1:idx+1], inorder[:idx])
        #定義右子樹
        #右子樹對於preorder及inorder的定義均同，均是排除root及左子樹位置，剩餘的位置
        root.right = self.buildTree(preorder[idx+1:], inorder[idx+1:])
        return root
```
解題技巧:
preorder = root -> left -> right
inorder = left -> root -> right
以例題中:
![](https://i.imgur.com/WZQkysa.jpg)

preoder = [(3),9,20,15,7], [(20),15,7]
inorder = [9,(3),15,20,7], [15,(20),7]
括號為root
若要個別找出preorder及inorder的左子樹
inorder便是當前root的左半邊為其左子樹 >> ["9",(3),15,20,7], ["15",(20),7]
preorder則為當前root的後一個~左子樹node總數 >> [(3),"9",20,15,7], [(20),"15",7]

## 109. Convert Sorted List to Binary Search Tree
#### 2022/6/6
參考來源: https://blog.csdn.net/fuxuemingzhu/article/details/80785093
目的: 將排序過的list轉換成height balance的BFS
```python=
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def sortedListToBST(self, head: Optional[ListNode]) -> Optional[TreeNode]:
        # 將 head 的值搜集成 list (nums)
        nums = []
        while head:
            nums.append(head.val)
            head = head.next
        return self.helper(nums)
    #helper用來分支root
    def helper(self, nums):
        # 若list為空，return None
        if not nums:
            return None
        mid = len(nums)//2
        # list的中間element即為root
        root = TreeNode(nums[mid])
        # 左子樹則為中間element以前的elements
        root.left = self.helper(nums[:mid])
        # 右子樹則為中間element以後的elements
        root.right = self.helper(nums[(mid+1):])
        return root
```
## 199. Binary Tree Right Side View
#### 2022/6/10
參考來源: https://www.youtube.com/watch?v=d4zLyf32e3I&t=439s&ab_channel=NeetCode
目的: 給定一個binary tree, 若有一個眼睛站在右側看去，把tree由上至下所看到的node加進一個list並回傳
```python=
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: Optional[TreeNode]) -> List[int]:
        res = []
        #將binary tree 用collections轉成 queue
        q = collections.deque([root])
        
        while q:
            #初始化原本要看到的node
            rightSide = None
            qLen = len(q)
            
            #用for loop一層一層看每個node
            for i in range(qLen): #[[1],2,3], qLen=2
                node = q.popleft() #root的部分
                #若node不為null
                if node:
                    rightSide = node #由於在for loop內，node會先為2, 接下來node再為3，直到for loop結束
                    q.append(node.left)
                    q.append(node.right) ##由於rightSide要取到for loop最尾端的node，所以右子樹會放在list的最後面
            #當for loop跑完時，此時的rightSide就是for loop最後一個迴圈的node，也就是從右側看過去的那個node
            if rightSide:
                res.append(rightSide.val)
        return res
```


