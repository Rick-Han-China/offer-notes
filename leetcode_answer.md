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
下边写错了，不知道为啥，输入为3就不对了
```C++
class Solution {
public:
    bool judgeSquareSum(int c) {
        int p1 = 0;
        int p2 = (int) sqrt(c);
        while(p1<=p2)
        {
            if(p1 ^ 2 + p2 ^ 2 == c) return true;
            else if(p1 ^ 2 + p2 ^ 2 < c) p1++;
            else p2--;
        }
        return false;
    }
};
```
