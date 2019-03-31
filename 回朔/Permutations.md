# Permutations

>Given a collection of distinct integers, return all possible permutations.

>Example:
```
Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
Solution:依然使用回朔的方法进行了解决，进行回朔的条件就是result的长度和输入数组nums的长度相同时进行回朔。
```python
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        result = []
        results = []
        def DFS(results,result,nums):
            if len(result)==len(nums):
                results.append(copy.deepcopy(result))
                return
            for i in nums:
                if i in result:	#判断是否已经包含了元素i
                    continue
                result.append(i)
                DFS(results,result,nums)
                
                result.pop()
        DFS(results,result,nums)
        return results
```