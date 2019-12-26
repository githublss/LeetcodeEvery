Binary Search
===
> Given a sorted (in ascending order) integer array nums of n elements and a target value, write a function to search target in nums. If target exists, then return its index, otherwise return -1.


Example 1:
```
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4
```
Example 2:  
```
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

Note:

You may assume that all elements in nums are unique.
n will be in the range [1, 10000].
The value of each element in nums will be in the range [-9999, 9999].  
题意：使用二分查找查找给定的元素  
方法：使用折半查找的方法来查找目标值。
```C++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int low = 0,heigh = nums.size()-1;
        while(low <= heigh){
            int mid = (low+heigh)/2;
            if(nums[mid] > target)
                heigh = mid - 1;
            if(nums[mid] < target)
                low = mid + 1;
            if(nums[mid] == target)
                return mid;
        }
        return -1;
    }
};
```
参考：[二分查找扩展](https://www.cnblogs.com/ider/archive/2012/04/01/binary_search.html)  
扩展：二分查找不仅可以用来进行查找目标值，还可以用来1）**查找上届和下届，**2）**找寻区域，**3）**在轮转后有序的数组上使用二分查找**。