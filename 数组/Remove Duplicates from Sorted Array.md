Remove Duplicates from Sorted Array
===
>Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
```
Example 1:

Given nums = [1,1,2],
Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the returned length.

Example 2:

Given nums = [0,0,1,1,1,2,2,3,3,4],
Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.
It doesn't matter what values are set beyond the returned length.
```
题意：将数组中重复的元素进行删除,最后返回数组的长度。与Remove Element题目的区别是，不是删除指定的值，而是删除数组中重复的元素。
方法：思路和Remove Element的一样，前面有个哨兵负责挖地雷，后面的哨兵负责道路基础建设，remove Element的建设哨兵是负责建设自己的脚下，这里的哨兵负责建设自己前面的一个元素。只有当前方哨兵传过来的值与自己脚下的值不一样的时候才将传过来的值铺到自己的前面。
```C++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()==0)
            return 0;
        int j = 0;
        for(int i=1;i<nums.size();i++){
            if(nums[j]!=nums[i]){
                nums[++j]=nums[i];
            }
        }
        return j+1;
    }
};
```