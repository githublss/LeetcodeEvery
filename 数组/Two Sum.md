# Two Sum
>Given an array of integers, return indices of the two numbers such that they add up to a specific target.

>You may assume that each input would have exactly one solution, and you may not use the same element twice.

```
Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
solution:
自己首先想到的是暴力法，参考人家的，人家是遍历一次的过程中建立一个字典，提高了查询速度
```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        # (1)暴力法
        # i=0
        # j=0
        # for i in range(len(nums)):
        #     for j in range(len(nums)-i-1):
        #         if (target==nums[i]+nums[i+j+1]):
        #             return [i,i+j+1]
        
        # (2)参考别人
        map={}
        for i in range(len(nums)):
            m = target - nums[i]
            if m in map:
                return [map[m],i]
            else:
                map[nums[i]] = i
        return []
```
使用C++模板库中的unordered_map<>建立一个哈希表，使得时间复杂度为O（n）。
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> result;
        if(nums.size()<=1)
            return result;
        unordered_map<int,int> myMap;
        for(int i=0;i<nums.size();i++){
            myMap[nums[i]] = i;
        }
        for(int i=0;i<nums.size();i++){
            int another = target - nums[i];
            if(myMap.find(another) != myMap.end()){
                if(myMap[another] == i) // 为了防止出现某个数是target的两倍的情况
                    continue;
                result.push_back(i);
                result.push_back(myMap[another]);
                break;
            }
        }
        return result;
    }
};
```