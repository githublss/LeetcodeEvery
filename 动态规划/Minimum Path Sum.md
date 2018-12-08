# Minimum Path Sum

>Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

>Note: You can only move either down or right at any point in time.
```
Example:

Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.
```

Solution:此题依然是动态规划的问题，可是说是Unique Paths和Unique PathsII的进化版，前面两道题是求路径的数量，而这道题是求所有路径中的最小值，和前面的题目具有层层递进的关系。<br>

dp[i][j]最优解:从左侧和上侧选出最小的值,加上本点对应的值,即是到达本点的最小值:dp[j+1][i+1] = min(dp[j][i+1],dp[j+1][i])+grid[j+1][i+1]<br>
递归的定义最优解:dp中每一个点的值,都是最小值.<br>
方法:备忘录自顶向下,<br>
输出最优解.

前面的dp用来记录路径的数量,这里的dp用来记录到达dp[i][j]的最小值,
```python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        n = len(grid)	#行数
        m = len(grid[0])	#列数
        dp = [[0 for i in range(m)] for j in range(n)]
        dp[0][0] = grid[0][0]
        for i in range(m-1):
            dp[0][i+1] = grid[0][i+1]+dp[0][i]
        for i in range(n-1):
            dp[i+1][0] = grid[i+1][0]+dp[i][0]
        for i in range(m-1):
            for j in range(n-1):
                dp[j+1][i+1] = min(dp[j][i+1],dp[j+1][i])+grid[j+1][i+1]
        return dp[n-1][m-1]
```
下面是用时最短的提交方案.可以看出他是直接在grid上进行的操作,所以用时上面要比我的要短.
```python
class Solution(object):
    def minPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """
        if grid is None:
            return 0
        rows = len(grid)
        cols = len(grid[0])
        if cols == 0:
            return 0
        
        for i in range(1, cols):
            grid[0][i] += grid[0][i - 1]
        for i in range(1, rows):
            grid[i][0] += grid[i - 1][0]
        for i in range(1, rows):
            for j in range(1, cols):
                grid[i][j] += min(grid[i - 1][j], grid[i][j - 1])
        return grid[-1][-1]
```