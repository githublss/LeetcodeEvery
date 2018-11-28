# Unique Paths

>A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).
The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).
How many possible unique paths are there?

![Alt](https://github.com/githublss/image/blob/master/leetimage/UniquePaths.png)

>Above is a 7 x 3 grid. How many possible unique paths are there?

>Note: m and n will be at most 100.
```
Example 1:

Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right
Example 2:

Input: m = 7, n = 3
Output: 28
```
Solution:看到题目的第一步，按照动态规划的思路来思考。 <br>
因为机器人只能向右和向下走，到达第一行格子都只有一种走法:dp[0][]=1,到达第一列格子只有一中走法:dp[][0]=1。<br>
那么到达一个格子的路线数，就应该是左侧格子路线加上上侧格子的路线的和：dp[i][j] = dp[i-1][j]+dp[i][j-1]。<br>
但是这里不用找出最优解，而是找出了所有的解。采用备忘录的方法。<br>

```python
class Solution(object):
    def uniquePaths(self, m, n):
        """
        :type m: int
        :type n: int
        :rtype: int
        """
        dp = [[0 for i in range(m)] for j in range(n)]
        for i in range(m):
            dp[0][i] = 1
        for i in range(n):
            dp[i][0] = 1
        for i in range(m-1):
            for j in range(n-1):
                dp[j+1][i+1] = dp[j+1][i]+dp[j][i+1]
        return dp[n-1][m-1]
```