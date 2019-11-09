Basic Calculator II
===

Implement a basic calculator to evaluate a simple expression string.  

The expression string contains only non-negative integers, +, -, *, / operators and empty spaces . The integer division should truncate toward zero.

Example 1:
```
Input: "3+2*2"
Output: 7
```
Example 2:
```
Input: " 3/2 "
Output: 1
```
Example 3:
```
Input: " 3+5 / 2 "
Output: 5
```
Note:

You may assume that the given expression is always valid.  
Do not use the eval built-in library function.  
题目翻译：
实现一个基础的计算器，来计算一个简单的字符串表达式。表达式中只含有正数和‘+’、‘-’、‘*’，‘、’基本运算符。整数除法向零取整。  
不可以使用内置的eval函数。

实现思路：  
参考函数: [string常用函数](https://www.cnblogs.com/xFreedom/archive/2011/05/16/2048037.html)  
使用string内置函数find_first_not_of(),来获取不是空格的位置。

代码实现：
```C++
class Solution {
public:
    int calculate(string s) {
        if(s.empty())
            return 0;
        int result =0,num =0,inner_result = 0;
        char op = '+';
        char ch;
        for(int i=s.find_first_not_of(' ');i<s.size();i=s.find_first_not_of(' ',i)){
            ch = s[i];
            
            if(ch >= '0' && ch <= '9'){
                num = ch - '0';
                while(++i<s.size() && s[i]>='0' && s[i]<='9'){
                    num = num * 10 + (s[i] - '0');
                }
                switch(op){
                        case('+'):
                        inner_result += num;
                        break;
                        
                        case('-'):
                        inner_result -= num;
                        break;
                        
                        case('*'):
                        inner_result *= num;
                        break;
                        
                        case('/'):
                        inner_result /= num;
                        break;
                }
            }
            else{
                if(ch == '+'||ch=='-'){
                    result += inner_result;
                    inner_result = 0;
                }
                op = s[i++];
            }
            
        }
        return result + inner_result;
    }
};
```
讨论区简洁方法：
```C++
class Solution {
public:
    int calculate(string s) {
        istringstream in('+' + s + '+');
        long long total = 0, term = 0, n;
        char op;
        while (in >> op) {
            if (op == '+' or op == '-') {
                total += term;
                in >> term;
                term *= 44 - op;
            } else {
                in >> n;
                if (op == '*')
                    term *= n;
                else
                    term /= n;
            }
        }
        return total;
    }
};
```