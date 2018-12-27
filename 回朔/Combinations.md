# Combinations

>Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

Example:
```
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]
```
sulotion:这是做的第一道回朔的题目，感觉还是有些难度的，但是万事开头难，随着对回朔的了解相信会慢慢对这类问题游刃有余。
首先求n个数中的k个数的combine,然后在求n-1个数中k-1个数的combine。
```python
class Solution(object):
    def combine(self, n, k):
        """
        :type n: int
        :type k: int
        :rtype: List[List[int]]
        """
        results = []
        result = []
        def DFS(results, result, start, n, k):
            if(k==len(result)):
                results.append(copy.deepcopy(result))	# python append()与深拷贝、浅拷贝应该注意，此处有一个大坑
                return  
            for i in range(start,n+1,1):
                result.append(i)
                DFS(results, result, i+1, n, k)
                result.pop()
        
        DFS(results, result, 1, n, k)
        return results
```