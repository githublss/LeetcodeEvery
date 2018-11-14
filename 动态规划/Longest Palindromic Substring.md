#  Longest Palindromic Substring
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
solution:第一次还是先想到的是暴力法(没有通过时间的限制)，后面又使用了动态规划，但是运行时间不是很理想，有待改进
![Alt](https://github.com/githublss/image/blob/master/leetimage/dongTaiGH.jpg)

```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        # 暴力法，总是最先想到的
        # def isRevrse(s):
        #     if(s==s[::-1]):
        #         return True
        #     else:
        #         return False
        # maxlen = 0
        # maxi = 0
        # for i in range(len(s)):
        #     for j in range(len(s)-i+1):
        #         if(isRevrse(s[i:i+j]) & (j > maxlen)):
        #             maxlen = j
        #             maxi = i
        # return s[maxi:maxi+maxlen]
        ### 动态规划一
        dp=[[0 for i in range(len(s))] for j in range(len(s))]
        maxLen = 1
        left = 0
        for i in range(len(s)): #初始化
            dp[i][i]=1
            left = i
        for i in range(len(s)-1): #初始化
            if s[i]==s[i+1]:
                dp[i][i+1]=1
                left = i
                maxLen = 2
        for l in range(3,len(s)+1,1):     # 当前字串的长度
            for i in range(0,len(s)-l+1,1):  # 当前字串的起始位置
                j = i + l -1
                if (dp[i+1][j-1]==1 and s[i]==s[j]):
                    dp[i][j] = 1
                    left = i
                    maxLen = l
        return s[left:left+maxLen]
```