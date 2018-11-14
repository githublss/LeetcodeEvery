# Add Two Numbers
>You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

>You may assume the two numbers do not contain any leading zero, except the number 0 itself.

```
Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```
Solution:虽然给的都是没有头节点的链表，并且接收的也是没有头节点的链表，但是可以创建一个具有头节点的链表，然后返回头节点的next，既可以达到目的
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        result = ListNode(0)
        temp =result
        jinwei = 0
        while l1 or l2:
            x = l1.val if (l1!=None) else 0
            y = l2.val if (l2!=None) else 0
            sum = jinwei + x + y
            jinwei = sum/10
            temp.next =ListNode(sum%10)
            if l1:
                l1 = l1.next
            if l2:
                l2 = l2.next
            temp = temp.next
        if jinwei!=0:
            temp.next = ListNode(jinwei)
        return result.next
```