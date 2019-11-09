Sort an Array
===
Given an array of integers nums, sort the array in ascending order.

 
```
Example 1:

Input: nums = [5,2,3,1]
Output: [1,2,3,5]
Example 2:

Input: nums = [5,1,1,2,0,0]
Output: [0,0,1,1,2,5]
```
题意：此题可以使用多种排序算法进行解答，算是数据结构中的基础题目。
方法：分别尝试使用简单选择排序、直接插入排序、快速排序方法来解决,但是由于简单选择排序和直接插入排序的时间复杂度比较高，没有通过所有的测试用例。
```C++
class Solution {
public:
    vector<int> sortArray(vector<int>& nums) {
        
        // selectSort(nums);
        // insertSort(nums);
        quickSort(nums,0,nums.size()-1);
        return nums;
        
    }
    // 简单选择排序
    void selectSort(vector<int>& nums){
        // 1.使用选择排序,由于时间复杂度为N方，测试用例通过率为9/10.
        
        int i,j;
        int selected,temp;
        for(i=0;i<nums.size()-1;i++){
            selected = nums[i];
            for(j=i;j<nums.size();j++){
                if(selected>nums[j]){
                    temp = selected;
                    selected = nums[j];
                    nums[j] = temp;
                }
            }
            nums[i] = selected;
        }
    }
    // 直接插入排序
    void insertSort(vector<int>& nums){
        // 2.使用直接插入排序，也是由于时间复杂度为N方，测试用例通过了9/10
        int i,j,k;
        int temp;
        for(i=1;i<nums.size();i++){
            for(j=i-1;j>=0;j--){    // 为元素a[i]，在前面找到合适的插人位置（j的后面）
                if(nums[j]<nums[i]){
                    break;
                }
            }
            if(j != i-1){
                // 将比a[i]大的数向后移
                temp = nums[i];
                for(k=i-1;k>j;k--){  
                    nums[k+1] = nums[k];
                }
                nums[j+1] = temp;   //将a[i]放到j的后面。
            }
            
        }
    }
    // 快速排序
    void quickSort(vector<int>& nums,int l,int h){
            if(l < h){
                int pivot = nums[l];
                int i = l,j = h;
                while(i < j){
                	// 从后向前找比pivot小的数。
                    while(i<j && nums[j]>pivot){
                        j--;
                    }
                    if(i<j)	
                        nums[i++]=nums[j]; 
                    // 从前往后找比pivot大的数。
                    while(i<j && nums[i]<pivot){
                        i++;
                    }
                    if(i<j)
                        nums[j--] = nums[i];
                }
                // 最后将pivot的值放到分割点上
                nums[i] = pivot;
                // 分治递归排序
                quickSort(nums,l,i-1);
                quickSort(nums,j+1,h);
            }
        }
};
```