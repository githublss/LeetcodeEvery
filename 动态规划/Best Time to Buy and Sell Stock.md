# Best Time to Buy and Sell Stock
>Say you have an array for which the ith element is the price of a given stock on day i.

>If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit.

>Note that you cannot sell a stock before you buy one.

```
Example 1:

Input: [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
             Not 7-1 = 6, as selling price needs to be larger than buying price.

Example 2:

Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.
```
solution:此题与上一道题的不同之处是最多只允许进行一次买卖
```python
class Solution(object):
    def maxProfit(self, prices):
        """
        :type prices: List[int]
        :rtype: int
        """
        # (1)暴力法，也是最容易想到的
        # maxResult = 0
        # for i in range(len(prices)):
        #     for j in range(len(prices)-i-1):
        #         if(prices[j+i+1]-prices[i] > maxResult):
        #             maxResult = prices[j+i+1]-prices[i]
        # return maxResult
        
        # (2)遍历一次，使用minP来记录交易中的最低价格，遍历找到最大利润值
        minP = sys.maxint   # python3中用 sys.maxsize来获取最大整数
        maxP = 0
        for i in range(len(prices)):
            if (prices[i] < minP):
                minP = prices[i]
            elif(prices[i] - minP > maxP):
                maxP = prices[i] - minP
        return (0 if maxP<0 else maxP)
```