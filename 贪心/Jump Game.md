Jump Game
===
Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Determine if you are able to reach the last index.

**Example 1:**

>Input: [2,3,1,1,4]
Output: true
Explanation: Jump 1 step from index 0 to 1, then 3 steps to the last index.

**Example 2:**

>Input: [3,2,1,0,4]
Output: false
Explanation: You will always arrive at index 3 no matter what. Its maximum
             jump length is 0, which makes it impossible to reach the last index.
Solution:使用贪心法来进行解决。当到下一步时，让可走的步数减一，同时看下一步的大小是否大于可走步数，如果大于就更新可走步数，否则继续使用前面记录下来的可走步数。
```python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        numsLen = len(nums)
        i = 0
        maxJump = 0
        mark = False
        if numsLen == 1:
            return True
        while(i<numsLen):
            if nums[i] > maxJump:
                maxJump = nums[i]
            if maxJump == 0:
                break;
            # print i,i+maxJump
            if (i + maxJump) >= numsLen-1:
                mark = True
                break
            maxJump -= 1
            i += 1
        return mark
```
Solution2:仿照这C++版的写了一个Python的另一个办法，通过定义一个可以到达的最远距离reach，最后来判断最远可以到达的距离reach是否等于n。
```python
class Solution(object):
    def canJump(self, nums):
        """
        :type nums: List[int]
        :rtype: bool
        """
        n = len(nums)
        reach = 0
        i = 0
        while (i<n and i<=reach):
            reach = max(nums[i]+i, reach)
            i+=1
        return i == n
            
```