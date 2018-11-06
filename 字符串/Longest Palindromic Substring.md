#Longest Palindromic Substring

>Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.
```
Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.

Example 2:

Input: "cbbd"
Output: "bb"
```

a sample solution(O(n2))
容易想到但是没有通过测试案例的时间限制

```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        def isRevrse(s):
            if(s==s[::-1]):
                return True
            else:
                return False
        maxlen = 0
        maxi = 0
        for i in range(len(s)):
            for j in range(len(s)-i+1,0,-1):
                if(isRevrse(s[i:i+j]) & (j > maxlen)):
                    maxlen = j
                    maxi = i

        return s[maxi:maxi+maxlen]
```
动态规划的核心元素：最优子结构，边界，状态转移方程式