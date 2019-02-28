# Letter Combinations of a Phone Number

>Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

>A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![Alt](https://github.com/githublss/image/blob/master/leetimage/elephone-keypad2.svg.png)

Example:
```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```
Note:

Although the above answer is in lexicographical order, your answer could be in any order you want.

方法一：通过回朔法，来解决。
现在看回朔就是将整个解题过程看成对一棵一颗树的遍历，如果有满足条件的就将遍历点添加到结果集中。一旦发现不满足条件就停止向下遍历。
```python
class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        zimus = {2:'abc',3:'def',4:'ghi',5:'jkl',6:'mno',7:'pqrs',8:'tuv',9:'wxyz'}
        every = []		# 用来存放digits所对应的字母组
        results = []	# 用来存放最终的结果
        result = ''		# 用来存放每种临时的可能值
        l = len(digits)
        if l == 0:
            return []
        for i in digits:
            every.append(zimus[int(i)])
        def DFS(every, results, result,level):	# level是用来指代digit中的第几个数
            if(len(result)==l):
                results.append(copy.deepcopy(result))
                return
            for i in every[level]:
                result = result + i
                DFS(every,results,result,level+1)
                result = result[:-1]
        DFS(every,results,result,0)
        return results
```
方法二：不使用回朔法，而使用组合的方法，生成结果。
```python
class Solution(object):
    def letterCombinations(self, digits):
        """
        :type digits: str
        :rtype: List[str]
        """
        l = [0, 1, 'abc', 'def', 'ghi', 'jkl', 'mno', 'pqrs', 'tuv', 'wxyz']
        if len(digits) == 0:
            return []
        result = ['']
        for i in range(len(digits)):
            letters = l[int(digits[i])]
            result = [rr+r for rr in result for r in letters]
        return result
```