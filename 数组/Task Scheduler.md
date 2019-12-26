Task Scheduler任务调度
===
>Given a char array representing tasks CPU need to do. It contains capital letters A to Z where different letters represent different tasks. Tasks could be done without original order. Each task could be done in one interval. For each interval, CPU could finish one task or just be idle.
However, there is a non-negative cooling interval n that means between two same tasks, there must be at least n intervals that CPU are doing different tasks or just be idle.
You need to return the least number of intervals the CPU will take to finish all the given tasks.

 

Example:
```
Input: tasks = ["A","A","A","B","B","B"], n = 2
Output: 8
Explanation: A -> B -> idle -> A -> B -> idle -> A -> B.
```

**Note:**

The number of tasks is in the range [1, 10000].
The integer n is in the range [0, 100].  
题意：（任务调度）给定一个用字符数组表示的 CPU 需要执行的任务列表。其中包含使用大写的 A - Z 字母表示的26 种不同种类的任务。任务可以以任意顺序执行，并且每个任务都可以在 1 个单位时间内执行完。CPU 在任何一个单位时间内都可以执行一个任务，或者在待命状态。
然而，两个相同种类的任务之间必须有长度为 n 的冷却时间，因此至少有连续 n 个单位时间内 CPU 在执行不同的任务，或者在待命状态。需要计算完成所有任务所需要的最短时间。  


**方法**：首先使用哈希表或者数组统计出每个任务的数量，然后进行排序，将数量最多的任务按照n个间隔进行排列，得到max_count（因为没个相同的任务之间要有n个时间的冷却时间）然后将剩余的任务按照要求插入到中间的间隔上，最后如果还有剩余的任务的话，将剩余的任务直接插入到max_count任务的中间，这样一定可以满足条件。  
任务时间最少公式: max(tcount[0]-1) * (n + 1) + count(tcount.begin(),tcount.end(),tcount[0]),tasks.size())
```c++
class Solution {
public:
    int leastInterval(vector<char>& tasks, int n) {
        int result = 0;
        vector<int> tcount (26,0);
        for(auto a : tasks){	//统计任务的数量
            tcount[a-'A']++;
        }
        sort(tcount.begin(),tcount.end(),greater<int>());
        result = (tcount[0]-1) * (n + 1) + count(tcount.begin(),tcount.end(),tcount[0]);
        if(result > tasks.size())
            return result;
        else{
            return tasks.size();
        }
    }
};
```