# Subsets II

>Given a collection of integers that might contain duplicates, nums, return all possible subsets (the power set).

>Note: The solution set must not contain duplicate subsets.

Example:
```
Input: [1,2,2]
Output:
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```
Solution1: 使用回朔的方法，由于不能有重复的集合，于是要比Sutsets题目多一个判断条件。<br>
Solution2：可以注意到集合此类排列组合的变化：[[]]->[[][1]]->[[][1][1,2][2]]->[[][1][1,2][2][1,2,3][1,3][2,3][3]]
			是在前一个的基础上，往每一个元素中添加一个新的元素，再加上原来的集合。如果不考虑重复元素集的话，后一个集合是前一个集合中元素的两倍。
```python
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        result = []
        results = []
        results.append([])
        def DFS(results,result,start):
            if len(result) == start+1:
                return
            for i in range(start,len(nums),1):
                result.append(nums[i])
                if result not in results:
                    results.append(copy.deepcopy(result))
                DFS(results,result,i+1)
                result.pop()
        DFS(results,result,0)
        return results
```

```python
class Solution(object):
    def subsetsWithDup(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        ret = [[]]
        for num in nums:
            ret += [item+[num] for item in ret if item+[num] not in ret]
        return ret
```