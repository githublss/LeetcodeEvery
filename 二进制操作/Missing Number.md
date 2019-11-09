Missing Number
===

>Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

Example 1:
```
Input: [3,0,1]
Output: 2
```
Example 2:
```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```
题目翻译：给一个从1到n的数组，中间缺少了一个数字。找到所缺少的那个数字。

方法1：先计算出从1到n的和，再计算出数组中元素的和，用第一次的数减去第二次所求的的值，得出的就是所丢失的值。  
但是当丢失的值是0的时候，两个数将相等。
```C++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int len = nums.size();
        int testSum = (len)*(1+len)/2;
        int sum = 0;
        for(int i:nums){
            sum += i;
        }
        if(sum==testSum){
            return 0;
        }
        else{
            return testSum-sum;
        }
    }
};
```
方法二：使用异或运算，两个整数进行异或时，相同得0,相异不为0.其运算时间要比方法一要快一些。cup所消耗的时钟周期中，异或运算要快于加法。
```C++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int len = nums.size();
        int sum = 0;
        for(int i=0;i<=len;i++) sum = sum^i;
        for(int i:nums) sum = sum^i;
        return sum;
    }
};
```