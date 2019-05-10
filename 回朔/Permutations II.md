#Permutations II

>Given a collection of numbers that might contain duplicates, return all possible unique permutations.

Example:
```
Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```
Solution:这道题目和上一道题目permutations十分类似，依然是使用回朔的方法来解决。<br>但是这道题目所给元素有重复值，但是要求最后的结果中不能有重复的结果，因此添加了一个标志数组，来标志数组中呢个元素是遍历过的。通过语句：if (used[i] == True) or (i>0 and nums[i]==nums[i-1] and used[i-1]==True) 来进行确定元素是否要进行遍历，效率比较高，要比使用语句：result in results效率高很多。<br>
速度可以相差十倍之多。
```python
class Solution(object):
    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        nums.sort()
        result = []
        results = []
        used = [False for i in range(len(nums))]
        def DFS(results,result,used):
            if len(result)==len(nums) :
                results.append(copy.deepcopy(result));
                return;
            for i in range(len(nums)):
                if (used[i] == True) or (i>0 and nums[i]==nums[i-1] and used[i-1]==True):
                    continue
                result.append(nums[i])
                used[i]=True
                DFS(results,result,used)
                used[i]=False
                result.pop()
        DFS(results,result,used)
        return results
```