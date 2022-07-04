# String

### 13. Roman to Integer
#### 2022/3/14
```python=
#最佳解
class Solution:
    def romanToInt(self, s: str) -> int:
        translations = {
            "I": 1,
            "V": 5,
            "X": 10,
            "L": 50,
            "C": 100,
            "D": 500,
            "M": 1000
        }
        number = 0
        s = s.replace("IV", "IIII").replace("IX", "VIIII")
        s = s.replace("XL", "XXXX").replace("XC", "LXXXX")
        s = s.replace("CD", "CCCC").replace("CM", "DCCCC")
        for char in s:
            number += translations[char]
        return number
str.replace(old, new[, max])
#我的解
class Solution:
    def romanToInt(self, s: str) -> int:
        t=0
        count=0
        dic={"I":'1', "V":'5', "X":'10', "L":'50', "C":'100', "D":'500', "M":'1000', "IV":'4', "IX":'9',                    "XL":'40', "XC":'90',"CD":'400', "CM":'900'}
        for i in s:
            t+=int(dic[i])
        if "IV" or "IX" in s:
            v=s.count("IV")
            x=s.count("IX")
            t=t-2*(v+x)
        if "XL" or "XC" in s:
            l=s.count("XL")
            c=s.count("XC")
            t=t-20*(l+c)
        if "CD" or "CM" in s:
            d=s.count("CD")
            m=s.count("CM")
            t=t-200*(d+m)
        return t  
```
### 67.Add Binary
#### 2022/3/26
```python=
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        res=""
        carry=0
        
        a, b = a[::-1], b[::-1]     ##a, b兩個字符以-1的方式切割前進，也就是從右到左
        
        for i in range(max(len(a), len(b))):
            digitA = ord(a[i]) - ord("0") if i < len(a) else 0 
            digitB = ord(b[i]) - ord("0") if i < len(b) else 0 ##確認a, b是否為0或1
            
            total = digitA + digitB + carry ##兩者相加
            char = str(total%2) ##結果必為2或非2的倍數，若非2，則餘數則留下1
            res = char + res #將餘數加進結果
            carry = total // 2  ##算出需加進位數
        if carry:
            res = "1" + res  #加入最終進位數
        return res
```
