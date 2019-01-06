# Combination Sum II

Given a collection of candidate numbers (candidates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

Each number in candidates may only be used once in the combination.

Note:

1. All numbers (including target) will be positive integers.
2. The solution set must not contain duplicate combinations.
Example 1:
```
Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```
Example 2:
```
Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]
```

solution1:这道题目与前面的题目combinations非常相似，不同是这道题目不能含有相同的元素，同一个元素不能使用超过一次，每一次向下遍历的时候要进行i+1的操作，因此在遍历的过程中要添加一个条件，if(i > current and candidates[i-1]==candidates[i]):，来判断是否是重复元素，要避免像[1,7],[1,7]这样的元素出现。
在这道题目中出现了一个长时间没有发现的错误，就是and的使用和&使用的区别，导致一直有重复元素的出现，以后要多加注意。
```python
class Solution(object):
    def combinationSum2(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        candidates.sort()
        results = []
        result = []
        def DFS(candidates,results,result,target,current):
            if(target-sum(result)<0):
                return
            elif(sum(result)-target==0):
                results.append(copy.deepcopy(result))
                return
            for i in range(current,len(candidates),1):
                if(i > current and candidates[i-1]==candidates[i]): //此处应注意&符号与and的使用
                    continue
                result.append(candidates[i])
                DFS(candidates,results,result,target,i+1)
                result.pop()
        DFS(candidates,results,result,target,0)
        return results
```