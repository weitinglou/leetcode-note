# leetcode-note

Topic
================
*   [Python module introduction](#pymodule)
    *   [**Collections**](#collections)

<h2 id="pymodule">Python module</h2>
<h3 id="collections">collections</h3>

collections.Counter
可以用來記數

相關題型

[387\. First Unique Character in a String]

 [387\. First Unique Character in a String]: https://leetcode.com/problems/first-unique-character-in-a-string/
這題可以使用collections.Counter將string產生hash array, 在string中只出現過一次的英文字母的counter value就會是1
##### Solution
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
