# Maximum Product Subarray

Given an integer array nums, find the contiguous subarray within an array (containing at least one number) which has the largest product.
```
Example 1:

Input: [2,3,-2,4]
Output: 6
Explanation: [2,3] has the largest product 6.
```
```
Example 2:

Input: [-2,0,-1]
Output: 0
Explanation: The result cannot be 2, because [-2,-1] is not a subarray.
```
Solution:此题与Maximum Subarray有些许类似，但此题目涉及到了正负数，因此要考虑到正负数两种情况。<br>

**最优子结构**：乘积最大的子序列<br>
**递归定义最优解的结构**：MaxSofar = max(MaxSofar, MaxEnd)，MaxEnd = max(nums[i+1], MaxEnd*nums[i+1])，MinEnd = min(nums[i+1], MinEnd*nums[i+1])，此次要比求最大子序列和的题目要多一个状态值，那就是最小值，一个负数乘以一个小的值要大于乘以一个大的值。<br>
**计算最优解**：MaxSofar<br>
**输入**：MaxSofar<br>
```python
class Solution(object):
    def maxProduct(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        MaxSofar = nums[0]
        MaxEnd  = nums[0]
        MinEnd = nums[0]
        for i in range(len(nums)-1):  
          # 乘以一个负数，大的数更小，小的的数更大，因此要交换一下最大数和最小数
            if(nums[i+1] < 0):
                MaxEnd,MinEnd = MinEnd, MaxEnd
            MinEnd = min(nums[i+1], MinEnd*nums[i+1])
            MaxEnd = max(nums[i+1], MaxEnd*nums[i+1])
            MaxSofar = max(MaxSofar, MaxEnd)
        return MaxSofar
```