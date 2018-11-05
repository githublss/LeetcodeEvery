# Reverse Words in a String III
>Given a string, you need to reverse the order of characters in each word within a sentence while still preserving whitespace and initial word order.

```
Example 1:

Input: "Let's take LeetCode contest"
Output: "s'teL ekat edoCteeL tsetnoc"

Note: In the string, each word is separated by single space and there will not be any extra space in the string.
```
resulted solution:
```python
class Solution(object):
    def reverseWords(self, s):
        """
        :type s: str
        :rtype: str
        """
        #自己的解答，与别人得解答
#         result = []
#         for i in s.split(" "):
#             result.append(i[::-1])
            
#         return (" ").join(result)
        return ' '.join([i[::-1] for i in s.split(' ')])
```