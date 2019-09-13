Add Binary
===

>Given two binary strings, return their sum (also a binary string).

The input strings are both non-empty and contains only characters 1 or 0.
```
Example 1:

Input: a = "11", b = "1"
Output: "100"
Example 2:

Input: a = "1010", b = "1011"
Output: "10101"
```
Solution:将二进制字符从字符中一个一个的取出来，跟字符‘0’进行相减的运算，就可以将字符转换为整数，进而来求余数和整除后的整数部分，还用到了string库中string的一些标准函数。

```C++
class Solution {
public:
    string addBinary(string a, string b) {
        string s;
        int index1 = a.size();
        int index2 = b.size();
        int carry = 0;
        int sum = 0;
        
        if(index1==0){
            return b;
        }
        if(index2==0){
            return a;
        }
        
        index1 = index1 - 1;
        index2 = index2 - 1;
        while(index1>=0 && index2>=0){
            sum = (a[index1] - '0')+(b[index2] - '0')+carry;
            carry = sum / 2;
            sum = sum % 2;
            s.insert(s.begin(),sum+'0');
            index1-=1;
            index2-=1;
        }
        while(index1>=0){
            sum = a[index1]-'0'+carry;
            carry = sum / 2;
            sum = sum % 2;
            s.insert(s.begin(),sum+'0');
            index1-=1;
        }
        while(index2>=0){
            sum = b[index2]-'0'+carry;
            carry = sum / 2;
            sum = sum % 2;
            s.insert(s.begin(),sum+'0');
            index2-=1;
        }
        if(carry==1){
            s.insert(s.begin(),carry+'0');
        }
        return s;
    }
};
```