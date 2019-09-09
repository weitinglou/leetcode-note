# leetcode-note

Topic
================
*   [Python module Related](#pymodule)
    *   [**Collections**](#collections)
*   [Math concept Related](#math)
    *   [**Sum**](#sum)

<h2 id="pymodule">Python module</h2>
<h3 id="collections">collections</h3>

1. collections.Counter
   可以用來做String每個letter出現次數的記數

相關題型

[387\. First Unique Character in a String]

 [387\. First Unique Character in a String]: https://leetcode.com/problems/first-unique-character-in-a-string/
##### Descrption
這題要在string中找到第一個獨特沒有重複的character,
例如: element 第一個沒有重複的character就是l

##### Solution
這題可以使用collections.Counter將string element產生成hash array, 並且計算每個keys在string中出現的次數存成value,
在string中只出現過一次的英文字母的counter value就會是1

```python
class Solution(object):
    def firstUniqChar(self, s):
        """
        :type s: str    eg, element
        :rtype: int
        """
        count = collections.Counter(s) 
        #count會變成hash array並且value會是每個character出現次數 
        #count = [e,3],[l,1][m,1][n,1][t,1]
        
        for i in range(0, len(s)):
            if count[s[i]] == 1:
                return i
        
        return -1
```
其他只使用collections.Counter就可解的題型
 [136\. Single Number]: https://leetcode.com/problems/single-number/
 
[451\. Sort Characters By Frequency]

 [451\. Sort Characters By Frequency]: https://leetcode.com/problems/sort-characters-by-frequency/
 ##### Description
 這題要將String中有出現的character按照出現頻率排列
 例如: tree 就要重新排列成 eetr
 
 ##### Solution
 這題一樣使用collections.Counter,並且搭配most_common,使用most_common可以針對每個key的value做排列
 會由value最大開始排序,most_common()可帶參數,例如most_common(3)就會印出頻率最高的3個character
 
 ```python
 class Solution(object):
    def frequencySort(self, s):
        """
        :type s: str    eg, tree
        :rtype: str
        """
        answer = ""
        c = collections.Counter(s)   # c = [t,1],[r,1],[e,2]
        c_common = c.most_common()   # c_common = [e,2],[t,1],[r,1] 
        for letter,count in c_common:
            answer += letter*count

        return answer
  ```

<h2 id="math">Math Concept Related</h2>
<h3 id="sum">Sum</h3>

相關題型

[268\. Missing Number]

 [268\. Missing Number]: https://leetcode.com/problems/missing-number/
##### Descrption
這題要在給定的array中找到消失的數字,例如在array中[3,0,1] 消失的數字為2

##### Solution
這題沒有特殊的解法,可以純粹從數學的概念中解題,只要將預期中的array總和減去出現過的數字,就可以找到消失的數字
在範例中預期的array總合為0+1+2+3=6, 減去3,0,1即可得到答案

```python
class Solution(object):
    def missingNumber(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        total = (len(nums)*(len(nums)+1))/2
        for i in nums:
            total = total - i
        return total
```
