Merge Sorted Array
===

Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

**Note:**

The number of elements initialized in nums1 and nums2 are m and n respectively.
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.
Example:
```
Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
```
**题意**：将两个顺序排列的数组进行合并，假设nums1中可以容纳下来自于nums2的元素，最后nums1中为合并的结果。  
**方法**：以前的办法是从nums1和nums2中从头到尾一个一个的取出元素进行比较，放到一个新的元素中，但是这里是要将数组2中的元素放到数组1中，不能从头进行操作。但是可以使用m和n作为指示哨兵，每一次将哨兵脚下比较大的数放到数组1的从后往前铺路的哨兵i的脚下。
```C++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        m--;
        n--;
        for(int i=m+n+1;i>=0;i--){
            if(m>=0 && n>=0){
                nums1[m] > nums2[n] ? nums1[i] = nums1[m--] : nums1[i]=nums2[n--];
                continue;
            }
            if(n>=0 && m<0){
                while(n>=0){
                    nums1[i--] = nums2[n--];
                }
            break;
            }
        }
    }
};
```