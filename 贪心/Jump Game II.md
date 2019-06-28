Jump Game II
===

		Given an array of non-negative integers, you are initially positioned at the first index of the array.

		Each element in the array represents your maximum jump length at that position.

		Your goal is to reach the last index in the minimum number of jumps.

Example:
```
Input: [2,3,1,1,4]
Output: 2
```
Explanation: The minimum number of jumps to reach the last index is 2.
    Jump 1 step from index 0 to 1, then 3 steps to the last index.
Note:

You can assume that you can always reach the last index.

**Solution**:此题与jupmGame I有些许相似，但是这个题目是要求得出到达终点的最小值，就是说一定可以到达终点，同样是用贪心的方法。
通过max(nextLoca, nums[i]+i)来得到最远可以到达的位置。curent用来记录当前可以到达的最远位置，nextLoca用来记录下次可以到达的最远位置。更新步数，将最大的**nextLoca**赋值给**curent**。重复进行操作，直到到达中点位置。
```python
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        numsLen = len(nums)
        step = 0        # 记录所走的步数
        curent = 0      # 记录当前可以到达的位置
        nextLoca = 0    # 记录当前位置与current位置之间可以到达的最远位置
        i = 0           # 记录遍历索引值
        while(i<numsLen):
            if curent >= numsLen-1:
                break
            while i<=curent:
                nextLoca = max(nextLoca,nums[i]+i)
                i += 1
            step += 1
            curent = nextLoca
        return step
```