# Combination Sum

>Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.
The same repeated number may be chosen from candidates unlimited number of times.

 1. All numbers (including target) will be positive integers.
 2. The solution set must not contain duplicate combinations.

Example 1:
```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```
Example 2:
```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```
Solution:虽然已经写了一道回朔的问题，但是刚开始写的时候还是有些懵，有点无从下手的感觉，看了一下别人的文章，发现这个回朔法是有些套路可寻的。函数所涉及到的参数不可能一次全部都考虑到，但是可以一边写一边添加自己所需要的参数。
过程：
1. 首先定义一个全局的变量results用来存放最终的结果，定义一个局部的全局变量，用来存放一个满足条件的组。
2. 定义回朔方法，DFS，candidates，target，result都添加进去，接着是写结束前进的条件target-sum(result),根据条件来判读是否进行回朔，如果是一个回朔点，就将此组数据添加到results中，否则就往下继续遍历。

```python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        candidates.sort()	# 先进行一下排序，保证从大到小排序
        results = []
        result = []
        def DFS(candidates, results, result, current, target):
            if(target -sum(result)< 0):
                return
            elif(target - sum(result) == 0):
                results.append(copy.deepcopy(result))	#使我们要的，就把数据添加到结果中去
                
            for i in candidates:
                if i>=current:	# 一方面保证没有重复的数据集，另一方面保证每一个元素，排序是从小到大
                    result.append(i)	# 试图添加一个点
                    DFS(candidates, results, result, i, target) #继续遍历并判断是否满足条件
                    result.pop()	# 进行回退
        DFS(candidates, results, result,candidates[0], target)
        return results
```