# leetcode-note

Topic
================
*   [Python module introduction](#pymodule)
    *   [**Collections**](#collections)

<h2 id="pymodule">Python module</h2>
<h3 id="collections">collections</h3>

collections.Counter
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
count = [e,3],[l,1][m,1][n,1][t,1]
```python
class Solution(object):
    def firstUniqChar(self, s):
        """
        :type s: str
        :rtype: int
        """
        count = collections.Counter(s)
        for i in range(0, len(s)):
            if count[s[i]] == 1:
                return i
        
        return -1
```

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
        :type s: str
        :rtype: str
        """
        answer = ""
        c = collections.Counter(s)
        c_common = c.most_common()
        for letter,count in c_common:
            answer += letter*count

        return answer
  ```
