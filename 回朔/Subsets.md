#Subsets

>Given a set of distinct integers, nums, return all possible subsets (the power set).

>Note: The solution set must not contain duplicate subsets.

Example:
```
Input: nums = [1,2,3]
Output:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```
Solution:python中数组作为函数参数时，是引用类型的传递。
	使用回朔的方法对满足要求的集合，添加到结果集中。
```python
class Solution(object):
    def subsets(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        result = []
        results = []
        results.append(copy.deepcopy(result))
        def DFS(result,results,start):	# start用来记录回朔结点在原列表中的索引值
            if len(result)==start+1:
                return
            for i in range(start,len(nums),1):
                result.append(nums[i])
                results.append(copy.deepcopy(result))
                DFS(result,results,i+1)
                result.pop()
        DFS(result,results,0)
        return results
```