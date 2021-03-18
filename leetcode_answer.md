# 167. Two Sum II - Input array is sorted
https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
返回的是vector<int>, 可以提前定义一个vector<int>用于返回，也可以返回时写一个vector<int>
N
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        vector<int> r;
        int p1 = 0;
        int p2 = numbers.size() - 1;
        while(p1 != p2)
        {
            if(numbers[p1] + numbers[p2] == target) 
            {
                r.push_back(p1+1);
                r.push_back(p2+1);
                return r;
            }
            else if(numbers[p1] + numbers[p2] < target) p1++;
            else p2--;
        }
        return r;
    }
};
```
# 633. Sum of Square Numbers
https://leetcode.com/problems/sum-of-square-numbers/
N
1.注意p1 p2初始化时要用long，否则会溢出，因为while中对p1 p2进行了乘方
2.乘方操作注意，要么pow,要么自己*自己，别用^
```C++
class Solution {
public:
    bool judgeSquareSum(int c) {
        long p1 = 0;
        long p2 = sqrt(c);
        
        while(p1<=p2)
        {
            if(p1*p1 + p2*p2 < c)
                p1++;
            else if(p1*p1 + p2*p2 > c)
                p2--;
            else
                return true;
        }
        return false;
    }
};
```
# 345. Reverse Vowels of a String
https://leetcode.com/problems/reverse-vowels-of-a-string/
N
两个点需要注意：
1.使用set容器，创建一个C风格字符串 2.交换后p1和p2需要移位，否则无法跳出循环3.注意count函数的使用方法，功能类似find，返回所查找元素出现的次数                                     
```C++
class Solution {
public:
    string reverseVowels(string s) {
        int p1 = 0;
        int p2 = s.size() - 1;
        set<char> dic = {'a','e','i','o','u','A','E','I','O','U'};
        while(p1 < p2)
        {
            while(p1<p2 and !dic.count(s[p1])) p1++;
            while(p1<p2 and !dic.count(s[p2])) p2--;
            if(p1<p2) swap(s[p1++], s[p2--]);
        }
        return s;
    }
};
```
