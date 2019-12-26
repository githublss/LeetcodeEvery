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
        // quickSort(nums,0,nums.size()-1);
        // bubbleSort(nums);
        // heapSort(nums);
        mergeSort(nums);
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
                        nums[i++] = nums[j]; 
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

    // 冒泡排序
    void bubbleSort(vector<int>& nums){
        // 时间复杂度同样为N方，只有9/10的用例通过
        for(int i=0;i<nums.size()-1;i++){   // 比较的趟数
            for(int j=0;j<nums.size()-i-1;j++){ // 每一趟中比较的次数
                if(nums[j]>nums[j+1]){
                    int temp = nums[j];
                    nums[j] = nums[j+1];
                    nums[j+1] = temp;
                }
            }
        }
    }

    // 堆排序
    void heapSort(vector<int>& nums){
        // 时间复杂度与快速排序相同，测试用例都可以通过
        int len = nums.size();
        heapBuild(nums,len);
        for(int newLen=len-1;newLen>0;newLen--){   
            swap(nums,newLen,0);
            // heapBuild(nums,newLen);
            heapAdjust(nums,0,newLen);
        }
    }
    void heapBuild(vector<int>& nums,int len){ // 建立大顶堆
        for(int i=len/2-1;i>=0;i--){    // 从最后一个非叶结点开始调整
            heapAdjust(nums,i,len);
        }
    }
    void heapAdjust(vector<int>& nums,int i,int end){
        int ded = i;
        int son = 2*i + 1;
        int largest = ded;
        if(son < end && nums[largest] < nums[son])
            largest = son;
        if(son+1 < end && nums[largest] < nums[son+1])
            largest = son + 1;
        if(largest != i){
            swap(nums,largest,i);
            heapAdjust(nums,largest,end);
        }
    }
    void swap(vector<int>& nums,int i,int j){
        int temp = nums[i];
        nums[i] = nums[j];
        nums[j] = temp;
    }

    // 归并排序,通过了所有测试用例，但是runtime是104ms，Memory usage是40M
    void mergeSort(vector<int>& nums){
        int len = nums.size();
        mergeSortUp2Down(nums,0,len-1);
    }
    void mergeSortUp2Down(vector<int>& nums,int start,int end){
        if(start >= end)
            return;
        int mid = (start + end) / 2;
        mergeSortUp2Down(nums,start,mid);
        mergeSortUp2Down(nums,mid+1,end);
        
        merge(nums,start,mid,end);
    }
    void merge(vector<int>& nums,int start,int mid,int end){
        vector<int> temp(end-start+1);
        int i = start,j = mid + 1, k = 0;
        while(i <= mid && j <= end){
            if(nums[i] < nums[j])
                temp[k++] = nums[i++];
            else
                temp[k++] = nums[j++];
        }
        while(i <= mid){
            temp[k++] = nums[i++];
        }
        while(j <= end){
            temp[k++] = nums[j++];
        }
        for(int h=0;h < k;h++){
            nums[h+start] = temp[h];
        }
    }
};
```