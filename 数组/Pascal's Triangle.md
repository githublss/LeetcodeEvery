Pascal's Triangle
===
>Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.
```
In Pascal's triangle, each number is the sum of the two numbers directly above it.

Example:

Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]
```
题意：输入一个数，输出一个帕斯卡三角形。
解决办法：通过观测可以看出，每一行的开头和结尾都是1，从第三行开始，中间的数字都是由上面的两个数字相加得到的，可以先初始化一个矩阵，然后进行计算。递推公式是：result[i][j]=result[i-1][j-1]+result[i-1][j]
```C++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> result;
        for(int i=1;i<=numRows;i++){	// 首先进行初始化
            result.push_back(vector<int>(i,1));
        }
        if(numRows>2){
            for(int i=2;i<numRows;i++){
                for(int j=1;j<i;j++){
                    result[i][j]=result[i-1][j-1]+result[i-1][j];	// 根据规律来生成三角形
                }
            }
        }
        return result;
    }
};
```