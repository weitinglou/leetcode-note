# leetcode-note

本份leetcode-note主要針對Top Interview Question所做的整理,

從這些問題中整理出可能會使用到的python module, built-in function

Topic
================
*   [Python module Related](#pymodule)
    *   [**Collections**](#collections)
*   [Python Built-in Related](#pybuiltin)
    *   [**Sort**](#sort)    
    *   [**Dict.get**](#dictget)
*   [Math concept Related](#math)
    *   [**Sum**](#sum)
    *   [**Recursive**](#recursive)
---------------------------------------
<h2 id="pymodule">Python module</h2>
<h3 id="collections">collections</h3>

1. collections.Counter
   可以用來做String每個letter出現次數的記數,也可用來算list中每個數字出現次數
   
   eg, string "element"經過collections.Counter會產生的dictionary為{"e":3, "l":1, "m":1, "n":1, "t":1}
   
   list \[2,3,4,3,5,2\] 經過collections.Counter會產生dictionary{2:2, 3:2, 4:1, 5:1}

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
[136\. Single Number]

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
---------------------------------------
<h2 id="pybuiltin">Python built-in Related</h2>
<h3 id="sort">Sort</h3>

Sort and Sorted
Python 內建有兩種可以做排序的function,分別是sort跟sorted,都可以用來排序list
差別在於sorted會回傳新的排序好的list,sort則會直接修改原本的list

相關題型

[41\. First Missing Positive]

 [41\. First Missing Positive]: https://leetcode.com/problems/first-missing-positive/
 ##### Descrption
 這題要在一個沒有排序過的list中,找到最小不存在在list中的正整數
 
 ##### Solution
 這題可以先將list排序過後,再對list做操作就會簡單許多,其中必須注意題目中有提到uses constant extra space
 所以這題使用的是sorted built-in function.
 
 ```python
 class Solution(object):
    def firstMissingPositive(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        cmp = 1     #最小出現在list中的整數從1開始
        sort_num = sorted(nums)
        for i in range(0,len(sort_num)):
            if sort_num[i] > 0:
                if sort_num[i] == (cmp-1):
                    cmp = cmp
                elif sort_num[i] != cmp:
                    return cmp
                else:
                    cmp += 1
        return cmp
 ```
 
 [4\. Median of Two Sorted Arrays]

 [4\. Median of Two Sorted Arrays]: https://leetcode.com/problems/median-of-two-sorted-arrays/
 ##### Descrption
 給兩個已經排序好的list,找到這兩個list的中間數
 
 ##### Solution
 把兩個list concat成一個後,使用sort built-in function 做排序,即可找到兩個list的中間數
 
 ```python
 class Solution(object):
    def findMedianSortedArrays(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: float
        """
        ans = nums1 + nums2
        ans = sorted(ans)
        ans_num = 0.0
        new_len = len(nums1) + len(nums2)

        if new_len %2 == 1:
            ans_num = ans[new_len/2]
        else:
            ans_num = (ans[new_len/2] + ans[(new_len/2) - 1])/2.0
        return ans_num
 ```
 
 <h3 id="dictget">Dict.get</h3>
 
 dict.get(key, default) 用在dictionary中,會返回指定key的value值,如果dictionary中沒有此key,則會返回default值
 
 eg, dict = {'Monday':1, 'Tuesday':2}
 dict.get('Monday',100) = 1
 dict.get('Wednesday',100) = 100
 
 相關題型

[350\. Intersection of Two Arrays II]

 [350\. Intersection of Two Arrays II]: https://leetcode.com/problems/intersection-of-two-arrays-ii/
 ##### Descrption
 給定兩個array,要求出他們的交集array
 
 ##### Solution
 這題配合前面介紹的module [**Collections**](#collections).Counter來解題,並且判斷兩個list中哪個list的長度較長
 
 eg, nums1 = \[1,2,2,1\]
    nums2 = \[2,2\]

 ```python
 class Solution(object):
    def intersect(self, nums1, nums2):
        """
        :type nums1: List[int]
        :type nums2: List[int]
        :rtype: List[int]
        """
        ans = []
        return_v = 0
        #collections.Counter會依據list中每個element出現的次數產生對應的dictionary
        count1 = collections.Counter(nums1)    #count1 = {1:2,2:2}
        count2 = collections.Counter(nums2)    #count2 = {2:2}
        
        if(len(nums1) > len(nums2)):    #判斷兩個list哪個長度較長,如果nums1較長則base取nums2來比
            for i in nums2:             #從nums2中的element來找是否nums1有包含此element
                return_v = count1.get(i,0)       #使用get來尋找count1中是否有key為i的element,如果有就會return非0的正數
                if return_v != 0:                #如果return value不是0就代表count1中有包含i element
                    ans.append(i)                #將此數append進answer中,並且將count1[i] -1
                    count1[i] -=1
        else:
            for i in nums1:
                return_v = count2.get(i,0)
                if return_v != 0:
                    ans.append(i)
                    count2[i] -=1
        return ans
 ```
 
---------------------------------------
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

<h3 id="recursive">Recursive</h3>

相關題型

[21\. Merge Two Sorted Lists]

 [21\. Merge Two Sorted Lists]: https://leetcode.com/problems/merge-two-sorted-lists/
##### Descrption
這題要將兩個排序過的list merge成一個排序過的list

##### Solution
這題使用遞迴的概念就可以解決,每次檢查兩個Node,回傳值比較小的Node,並且傳入下一個Node進行比對

```python
class Solution(object):
    def mergeTwoLists(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        if l1 == None: return l2    #如果Node l1為空節點則直接回傳l2
        if l2 == None: return l1    #如果Node l2為空節點則直接回傳l1
        
        if l1.val <= l2.val:    #如果l1節點的值小於l2節點的值就回傳l1,並且比較l1.next及l2節點哪個值較小
            l1.next = self.mergeTwoLists(l1.next, l2)    
            return l1
        else:    #如果l2節點的值小於l1節點的值就回傳l2,並且比較l2.next及l1節點哪個值較小
            l2.next = self.mergeTwoLists(l2.next, l1)
            return l2
```
