#Leetcode 总结：（start on 20181008）
##1015 德才论 （25 分）
>宋代史学家司马光在《资治通鉴》中有一段著名的“德才论”：“是故才德全尽谓之圣人，才德兼亡谓之愚人，德胜才谓之君子，才胜德谓之小人。凡取人之术，苟不得圣人，君子而与之，与其得小人，不若得愚人。”

>现给出一批考生的德才分数，请根据司马光的理论给出录取排名。

>输入格式：
输入第一行给出 3 个正整数，分别为：N（≤10
​5
​​ ），即考生总数；L（≥60），为录取最低分数线，即德分和才分均不低于 L 的考生才有资格被考虑录取；H（<100），为优先录取线——德分和才分均不低于此线的被定义为“才德全尽”，此类考生按德才总分从高到低排序；才分不到但德分到线的一类考生属于“德胜才”，也按总分排序，但排在第一类考生之后；德才分均低于 H，但是德分不低于才分的考生属于“才德兼亡”但尚有“德胜才”者，按总分排序，但排在第二类考生之后；其他达到最低线 L 的考生也按总分排序，但排在第三类考生之后。

>随后 N 行，每行给出一位考生的信息，包括：准考证号 德分 才分，其中准考证号为 8 位整数，德才分为区间 [0, 100] 内的整数。数字间以空格分隔。

>输出格式：
输出第一行首先给出达到最低分数线的考生人数 M，随后 M 行，每行按照输入格式输出一位考生的信息，考生按输入中说明的规则从高到低排序。当某类考生中有多人总分相同时，按其德分降序排列；若德分也并列，则按准考证号的升序输出。

输入样例：
```
14 60 80
10000001 64 90
10000002 90 60
10000011 85 80
10000003 85 80
10000004 80 85
10000005 82 77
10000006 83 76
10000007 90 78
10000008 75 79
10000009 59 90
10000010 88 45
10000012 80 100
10000013 90 99
10000014 66 60
输出样例：
12
10000013 90 99
10000012 80 100
10000003 85 80
10000011 85 80
10000004 80 85
10000007 90 78
10000006 83 76
10000005 82 77
10000002 90 60
10000014 66 60
10000008 75 79
10000001 64 90
```
```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-
# Created by lss on 2018/10/9

class Student(object):
    def __init__(self, id, deScore, caiScore):
        self.id = id
        self.deScore = deScore
        self.caiScore = caiScore
        self.Total = self.caiScore + self.deScore

def printStu(student):
    for i in range(len(student)):
        print student[i].id,student[i].deScore,student[i].caiScore

def sortStu(students):
    students.sort( reverse=True,cmp=lambda x,y:cmp(x.Total,y.Total)or
                    cmp(x.deScore,y.deScore)or cmp(y.id,x.id))  # 实现多重排序

def main():
    N, L, G= map(int,raw_input().split(' '))    # 一行输入多个值
    students = []
    for i in range(N):
        id, deScore, caiScore = map(int, raw_input().split(' '))
        students.append(Student(id,deScore,caiScore))
    success1 = []
    success2 = []
    success3 = []
    success4 = []
    for stu in students:
        if (stu.deScore >= G) & (stu.caiScore >=G):
            success1.append(stu)
        elif (stu.deScore >= G) & (stu.caiScore >=L):
            success2.append(stu)
        elif (stu.deScore >= L) & (stu.caiScore >=L):
            if stu.deScore >stu.caiScore:
                success3.append(stu)
            else:
                success4.append(stu)
    sortStu(success1)
    sortStu(success2)
    sortStu(success3)
    sortStu(success4)
    print len(success4)+len(success3)+len(success2)+len(success1)
    printStu(success1)
    printStu(success2)
    printStu(success3)
    printStu(success4)

if __name__ == '__main__':
    main()
```
##Minimum Depth of Binary Tree
>Given a binary tree, find its minimum depth.

>The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

>Note: A leaf is a node with no children.

>Example:

>Given binary tree [3,9,20,null,null,15,7]
```
	3
   / \
  9  20
    /  \
   15   7
```
return its minimum depth = 2.

```python
# Definition for a binary tree node.
# class TreeNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution(object):     # 感觉测试实例有问题，没有通过。[1,2]应该是输出1，但expected:2
    def minDepth(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        if root is None:
            return 0
        depth=1
        result=[root]
        while result:
            result2=[]	#放每一层的节点
            for each in result:
                if each.left:
                    result2.append(each.left)
                else:return depth
                if each.right:
                    result2.append(each.right)
                else:return depth
            depth+=1	#如果一层都不为空加1
            result = result2 	#更新根节点列表

```