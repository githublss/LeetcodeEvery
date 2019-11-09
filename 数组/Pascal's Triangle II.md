Pascal's Triangle II
===

Given a non-negative index k where k ≤ 33, return the kth index row of the Pascal's triangle.

Note that the row index starts from 0.


In Pascal's triangle, each number is the sum of the two numbers directly above it.
```
Example:

Input: 3
Output: [1,3,3,1]
```
**Follow up:**

Could you optimize your algorithm to use only O(k) extra space?
题意：此题与上一道生成三角形的题目的题意是类似的。但是这里只有能使用一个数组，而不能像之前一样来生成一个二维的数组
办法：由于要在一个数组上来进行操作，假如得出了第3层的数据，在计算第四层数据的时候：result[1]=result[0]+result[1],后面在计算result[2]=result[1]+result[2]的时候，result[1]已经被覆盖。
但是可以先计算出result[3]=result[3]+result[2],后面再计算result[2]=result[2]+result[1]的时候并不会影响对result[2]的计算，这样从后往前来计算。
![推导过程](https://raw.githubusercontent.com/githublss/image/master/image/20191101171941.png)

```C++
class Solution {
public:
    vector<int> getRow(int rowIndex) {
        vector<int> result(rowIndex+1, 1);  //对数组进行初始化
        if(rowIndex==0||rowIndex==1)
            return result;
        for(int i=2;i<=rowIndex;i++){
            for(int j=i;j>1;j--){
                result[j-1] = result[j-2] + result[j-1];    // 从后往前来对数组进行计算。
            }
        }
        return result;
    }
};
```