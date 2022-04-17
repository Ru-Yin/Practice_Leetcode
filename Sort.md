# Sort

### 349. Intersection of Two Arrays
#### 2022/3/26
```python=
#my answer:
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        lst=[]
        for i in set(nums1):
            if i in set(nums2):
                lst.append(i)
        return lst
#answer:
class Solution:
    def set_intersection(self, set1, set2):
        return [x for x in set1 if x in set2]
        
    def intersection(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """  
        set1 = set(nums1)
        set2 = set(nums2)
        
        if len(set1) < len(set2):
            return self.set_intersection(set1, set2)
        else:
            return self.set_intersection(set2, set1)
```
### 148. Sort List (medium)
#### 2022/3/30
https://alrightchiu.github.io/SecondRound/comparison-sort-merge-sorthe-bing-pai-xu-fa.html
### 350. Intersection of Two Arrays II
#### 2022/3/30
```python=
class Solution:
    def intersect(self, nums1: List[int], nums2: List[int]) -> List[int]:
        lst=[ ]
        lst1=set(nums1)
        lst2=set(nums2)
        for i in nums1:
            lst2=set(nums2)
            if i in lst2:
                lst.append(i)
                nums2.remove(i)
        return lst
```