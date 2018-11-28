# Unique Paths II

>A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

>The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

>Now consider if some obstacles are added to the grids. How many unique paths would there be?

![Alt](https://github.com/githublss/image/blob/master/leetimage/UniquePaths.png)

>An obstacle and empty space is marked as 1 and 0 respectively in the grid.

>Note: m and n will be at most 100.

Example 1:
```
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2
Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right
```
Solution:这一道题目与I题的区别是有了障碍，但是基本思路还是不变的。<br>
只是一旦碰到障碍即将通过此障碍点的路线数量设置为0.<br>
其他思路不变。
```python
class Solution(object):
    def uniquePathsWithObstacles(self, obstacleGrid):
        """
        :type obstacleGrid: List[List[int]]
        :rtype: int
        """
        n = len(obstacleGrid)
        m = len(obstacleGrid[0])
        dp = [[0 for i in range(m)] for j in range(n)]
        for i in range(m):
            if(obstacleGrid[0][i]==1):
                break;
            dp[0][i] = 1
        for i in range(n):
            if(obstacleGrid[i][0]==1):
                break;
            dp[i][0] = 1
        for i in range(m-1):
            for j in range(n-1):
                if(obstacleGrid[j+1][i+1]==1):
                    continue;
                dp[j+1][i+1] = dp[j+1][i]+dp[j][i+1]
        return dp[n-1][m-1]
```