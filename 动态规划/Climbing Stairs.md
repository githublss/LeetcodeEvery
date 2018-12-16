# Climbing Stairs

>You are climbing a stair case. It takes n steps to reach to the top.

>Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

>Note: Given n will be a positive integer.

Example 1:
```
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps
```
Example 2:
```
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step
```
Solution:可以看成是爬楼梯问题-----此题依然是一个动态规划问题，也可以看作是一个递归问题，因为最后到达楼顶有两种可能，分别是从倒数第一阶到的，倒数第二阶到的。那么问题的解就是到倒数第一层的个数加上到倒数第二层的个数。但是这个题目和斐波那契数列是如此的相像。<br>
**最优子结构**：此题目不涉及到最值问题<br>
**递归定义最优解的结构**：DP[i] = DP[i-1]+DP[i-2]，第一层和第二层的走法分别有一种和两种。<br>
**计算最优解**：DP中存储了到达每一阶的个数，作为一个记事本<br>
**输入**：DP中最后一个值，即为到达楼顶的值<br>
```python
class Solution(object):
    def climbStairs(self, n):
        """
        :type n: int
        :rtype: int
        """
        if n==1:
            return 1
        dp = [0 for i in range(n)]
        dp[0]=1	#初始化
        dp[1]=2	#初始化
        for i in range(2,n,1):
            dp[i] = dp[i-1] + dp[i-2]  
        return dp[n-1]
```