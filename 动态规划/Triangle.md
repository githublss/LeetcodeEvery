# Triangle

>Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

>For example, given the following triangle
```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```
>The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

>Note:

>Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.
Solution:
**最优子结构**：计算到达某个点的路径值时，从下面两个中选出路径和较小的一个和本点的值相加<br>
**递归定义最优解的结构**：dp[j] = min(dp[j],dp[j+1])+triangle[endLine-i-2][j]<br>
**计算最优解**：自底向上方法，dp作为一个记事本<br>
**输入**：dp[0]就是最小值<br>

```python
class Solution(object):
    def minimumTotal(self, triangle):
        """
        :type triangle: List[List[int]]
        :rtype: int
        """
        endLine = len(triangle)	# 求出一共有几层，最后一层有几个元素
        dp = triangle[endLine-1]	# 进行初始化，存储了从下面走到对应点的最短距离。
        for i in range(endLine):	#对每一层递归计算
            for j in range(endLine-i-1):	#对每一层的元素进行计算
                dp[j] = min(dp[j],dp[j+1])+triangle[endLine-i-2][j]	#计算
        return dp[0]
```