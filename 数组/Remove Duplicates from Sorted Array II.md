Remove Duplicates from Sorted Array II
===

>Given a sorted array nums, remove the duplicates in-place such that duplicates appeared at most twice and return the new length.
Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.
```
Example 1:

Given nums = [1,1,1,2,2,3],

Your function should return length = 5, with the first five elements of nums being 1, 1, 2, 2 and 3 respectively.

It doesn't matter what you leave beyond the returned length.
Example 2:

Given nums = [0,0,1,1,1,1,2,3,3],

Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.

It doesn't matter what values are set beyond the returned length.
```

```
Clarification:

Confused why the returned value is an integer but your answer is an array?

Note that the input array is passed in by reference, which means modification to the input array will be known to the caller as well.

Internally you can think of this:

// nums is passed in by reference. (i.e., without making a copy)
int len = removeDuplicates(nums);

// any modification to nums in your function would be known by the caller.
// using the length returned by your function, it prints the first len elements.
for (int i = 0; i < len; i++) {
    print(nums[i]);
}
```
题意：与之前的题目类似,但是这里每个数最多允许在数组中出现两次。
解决方法：当前方哨兵传过来的值与自己脚下的值不一样的时候才将传过来的值铺到自己的前面，并且使用count来记录下来有一个了，当前面的哨兵传过来的值与自己脚下的值一样的时候，就要看看count的值是多少，如果是1的话就放到自己的前面，并且用count记录下来自己有相同的两个数了。如果是2的话就不管它。
```C++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if(nums.size()==0)
            return 0;
        int j = 0, count = 1;
        for(int i=1;i<nums.size();i++){
            if(nums[j] != nums[i]){		// 传来的值与脚下的值不一样
                nums[++j] = nums[i];
                count = 1;
            }
            else if(nums[j] == nums[i] && count==1){	// 传来的值与脚下的值一样，但是只有一个
                count = 2;
                nums[++j] = nums[i];
            }
            // if(nums[j] == nums[i]){
            //     count += 1;
            //     if(count <= 2)
            //         nums[++j] = nums[i];
            // }
            // else{
            //     nums[++j] = nums[i];
            //         count = 1;
            // }
        }
        return j+1;
    }
};
```