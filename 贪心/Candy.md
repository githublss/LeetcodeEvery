Candy
===

There are N children standing in a line. Each child is assigned a rating value.

You are giving candies to these children subjected to the following requirements:

- Each child must have at least one candy.
- Children with a higher rating get more candies than their neighbors.

What is the minimum candies you must give?

Example 1:
```
Input: [1,0,2]
Output: 5
Explanation: You can allocate to the first, second and third child with 2, 1, 2 candies respectively.
```
Example 2:
```
Input: [1,2,2]
Output: 4
Explanation: You can allocate to the first, second and third child with 1, 2, 1 candies respectively.
             The third child gets 1 candy because it satisfies the above two conditions.
```
Solution:题目要求等级高的小朋友的糖果要比邻居小朋友的糖果的数量要多，所以可以进行两次遍历，一次从左到右，一次从右到左，按照如果遍历的小朋友的等级比前一个小朋友的等级高，就在前一个小朋友的基础上再加上一（当时当他们等级相同的时候，就不需要这么做，小朋友不会伤心吗？没办法，题目就是这么要求的。）
```C++
class Solution {
public:
    int candy(vector<int>& ratings) {
        vector<int> candys;
        candys.resize(ratings.size(),1);
        for(int i=1;i<ratings.size();i++){
            if(ratings[i]>ratings[i-1]){
                candys[i] = candys[i-1] + 1;
            }
        }
        for(int i=ratings.size()-2;i>=0;i--){
            if(ratings[i]>ratings[i+1] && (candys[i]<candys[i+1]+1)){
                candys[i] = candys[i+1] + 1;
            }
        }
        int sum = 0;
        for(auto i:candys){
            sum += i;
        }
        return sum;
    }
};
```