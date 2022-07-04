# Array

### 53. Maximum Subarray
#### 2022/03/08 
```python=
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        # lst_max=[]
        # m = max(nums)
        # lst_max.append(m)
        # n=2
        # for i in range(len(nums)):
        #     lst=[None]*n
        #     for j in range(n):
        #         if n<len(nums):
        #             n = n+1
        #         lst[j] = nums[i]
        #     s = sum(lst)
        #     lst_max.append(s)
        # return max(lst_max)
##別人解答
        maxSum=nums[0]
        curSum=0
        for n in nums:
            if curSum<0:
                curSum=0
            curSum+=n
            maxSum=max(maxSum,curSum)
        return maxSum
##最佳解:
class Solution:
    # @param A, a list of integers
    # @return an integer
    # 6:57
    def maxSubArray(self, A):
        if not A:
            return 0

        curSum = maxSum = A[0]
        for num in A[1:]:
            curSum = max(num, curSum + num)
            maxSum = max(maxSum, curSum)

        return maxSum
```
 
### 26. Remove Duplicates from Sorted Array
#### 2022/03/09 (一半別人提示)
```python=
class Solution:
    def removeDuplicates(self, nums: List[int]) -> int:
        index = 0
        for i in range(len(nums)):
            if i == 0 or nums[i]!=nums[i-1]:
                nums[index] = nums[i]
                index+=1
            # elif i != 0:
            #     if nums[i]!=nums[i-1]:
            #         nums[index] = nums[i]
            #         index+=1
        return index
```
### 717. 1-bit and 2-bit Characters
#### 2022/03/10
```python=
#array中只能排列出10, 11, 0這幾個數字，且array的最後一位要是0
class Solution:
    def isOneBitCharacter(self, bits: List[int]) -> bool:
        while True:
            if bits[0]==1:
                bits.pop(0)
                if len(bits)<=0:
                    return False
                bits.pop(0)
                if len(bits)<=0:
                    return False
            else:
                bits.pop(0)
                if len(bits)<=0:
                    return True
```
### 121. Best Time to Buy and Sell Stock
#### 2022/3/12
```python=
buy = prices[0]
lst=[]
for i in range(1, len(prices)):
    if prices[i]<buy:
        buy=prices[i]
        # print(buy)
    else:
        earn=int(prices[i])-int(buy)
        lst.append(earn)
if buy==prices[-1]  and len(lst)==0:
    return 0
else:
    return max(lst)
```
