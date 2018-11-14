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

solution:第一次还是先想到的是暴力法(没有通过时间的限制)，后面又使用了动态规划，但是运行时间不是很理想，有待改进<br>
动态规划步骤：<br>
矩阵NP初始值都为0<br>
首先是初始化(对角线NP[i][i]上都设置为1，以对角线上的元素为中心的回文长度都为奇数；有两辆相同的将对应的NP[i+1][i]<br>元素设置为1，以此两元素为中心的回文长度均为偶数)---><br>

![Alt](https://github.com/githublss/image/blob/master/leetimage/first.png)

然后是在初始化的基础上进行寻找---><br>
首先假设回文的长度为3，之后依次递增。如果中心的两侧的两个字符是相同的，将其规划进来，将NP中的对应位置设置为1，在进行的过程中用到了前面的结果，一定程度上提高了效率。<br>

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
        for l in range(3,len(s)+1,1):     # l表示当前要检测的字串串的长度
            for i in range(0,len(s)-l+1,1):  # i表示当前要检测的字符串的起始位置
                j = i + l -1                 # j表示当前要检测的字符串的尾位置
                if (dp[i+1][j-1]==1 and s[i]==s[j]):
                    dp[i][j] = 1
                    left = i
                    maxLen = l
        return s[left:left+maxLen]
```