Plus One
===

> Given a non-empty array of digits representing a non-negative integer, plus one to the integer.
The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.
You may assume the integer does not contain any leading zero, except the number 0 itself.
```
Example 1:

Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Example 2:

Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
```
题意：给一个以数组形式存储的整数，现在对这个整数加上1，就是要考虑进位的问题。
解决办法：考加法进位的问题。
```C++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        for(int i=digits.size()-1;i>=0;i--){
            if((digits[i]=(digits[i]+1)%10)!=0){
                break;
            }
            if(digits[0]==0){
                digits.insert(digits.begin(),1); //如果最后最高位也进位了，就在最高位前面插入一个1
            }
        }
        return digits;
    }
};
```