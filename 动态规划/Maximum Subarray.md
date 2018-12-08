# Maximum Subarray
>Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:
```
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.
Follow up:
```
>If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.

solution:很久以前看这道题目的时候，是通过暴力法来解决的，但是没有通过时间的限制。最近练习动态规划也是有了一点点的感觉，来把这道题重新解一次。
这个问题由Jon Bentley曾经讨论（1984年9月第27卷第9期ACM P885通讯）
以下是原文：
>
```
the paragraph below was copied from his paper (with a little modifications)

algorithm that operates on arrays: it starts at the left end (element A[1]) and scans through to the right end (element A[n]), keeping track of the maximum sum subvector seen so far. The maximum is initially A[0]. Suppose we've solved the problem for A[1 .. i - 1]; how can we extend that to A[1 .. i]? The maximum
sum in the first I elements is either the maximum sum in the first i - 1 elements (which we'll call MaxSoFar), or it is that of a subvector that ends in position i (which we'll call MaxEndingHere).

MaxEndingHere is either A[i] plus the previous MaxEndingHere, or just A[i], whichever is larger.
```
局部最优子结构：包含最后一个元素时的最大和字串，
最优解的值：MaxSofar = max(MaxSofar,MaxEnd){ MaxEnd = max(MaxEnd+nums[i],nums[i]), ManEnd可以看作辅助最优子结构 }，MaxSofar是目标，MaxEnd是从第一个元素一直遍历到第i个元素时，从第一个元素到第i个元素包含第i个元素时的最优解。（包含第i个元素方便后面的遍历，因为题目要求最优子序列是连续的，如果没有第i个元素后面的遍历将不方便包含后面元素的遍历进行）
计算最优解：自底向上
最优解：输出最大的MaxSofar

```python
class Solution(object):
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        count = len(nums)
        if count==0:
            return 0
        MaxEnd = nums[0]
        MaxSof = nums[0]
        for i in range(count-1):
            MaxEnd = max(MaxEnd+nums[i+1],nums[i+1])
            MaxSof = max(MaxSof,MaxEnd)
        return MaxSof
```
```python
class Solution(object):
    def maxSubArray(self, nums):
        # 下面和上面的思路时一样的，但是更加简洁高效
        count = len(nums)
        for i in range(1,count):
            if nums[i-1] > 0:
                nums[i] = nums[i] + nums[i-1]
        return max(nums)
```