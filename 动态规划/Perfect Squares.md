# Perfect Squares

>Given a positive integer n, find the least number of perfect square numbers (for example, 1, 4, 9, 16, ...) which sum to n.

Example 1:
```
Input: n = 12
Output: 3 
Explanation: 12 = 4 + 4 + 4.
```
Example 2:
```
Input: n = 13
Output: 2
Explanation: 13 = 4 + 9.
```
Solution(动态规划):看到这道题目时没有想出怎么来解答，在Discuss中看到了一个很好的解释：
```
dp[0] = 0 
dp[1] = dp[0]+1 = 1
dp[2] = dp[1]+1 = 2
dp[3] = dp[2]+1 = 3
dp[4] = Min{ dp[4-1*1]+1, dp[4-2*2]+1 } 
      = Min{ dp[3]+1, dp[0]+1 } 
      = 1				
dp[5] = Min{ dp[5-1*1]+1, dp[5-2*2]+1 } 
      = Min{ dp[4]+1, dp[1]+1 } 
      = 2
						.
						.
						.
dp[13] = Min{ dp[13-1*1]+1, dp[13-2*2]+1, dp[13-3*3]+1 } 
       = Min{ dp[12]+1, dp[9]+1, dp[4]+1 } 
       = 2
						.
						.
						.
dp[n] = Min{ dp[n - i*i] + 1 },  n - i*i >=0 && i >= 1
```
找到最优解的形式是重要的，后面就是利用前面求出的值动态构建。<br>
我们能够记录已经找到的最小组合，那么稍大一些的数只需要在此基础上添加若干个完全平方数即可。这里面就包含了动态规划
的思想。

```python
class Solution(object):
    def numSquares(self, n):
        """
        :type n: int
        :rtype: int
        """
        import sys
        dp = [sys.maxint]*(n+1)
        dp[0] = 0
        for i in range(1,n+1,1):
            j = 1
            while((i - j * j) >= 0):
                dp[i] = min(dp[i-j*j]+1,dp[i])
                j += 1
        return dp[n]
```