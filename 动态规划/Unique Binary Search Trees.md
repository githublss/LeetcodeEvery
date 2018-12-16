# Unique Binary Search Trees

>Given n, how many structurally unique BST's (binary search trees) that store values 1 ... n?

>Example:
```
Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```
Solution:首先要想到二叉树的性质：左侧的分支都小于根节点，右侧的分支都大于根节点。1,2,3组成的二叉树个数和4,5,6组成的个数是相等的。<br>
这就提示我们只需要记录下一定个数的节点数所能形成的二叉树个数。<br>
当有i个数时，若左侧有k个数，右侧有i-k-1个数，递推公式是：dp[i]=sum(dp[j]+dp[i-j-1])<br>
也是采用的自底向上方法。<br>
dp[n]既是n个数时的二叉树的个数。<br>
```python
class Solution(object):
    def numTrees(self, n):
        """
        :type n: int
        :rtype: int
        """
        dp = [0 for i in range(n+1)]
        dp[0]=1
        dp[1]=1
        for i in range(2,n+1,1):
            for j in range(i):
                dp[i] += dp[j]*dp[i-j-1]
        return dp[n]
```