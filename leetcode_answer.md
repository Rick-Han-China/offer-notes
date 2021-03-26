# 双指针
## 167. Two Sum II - Input array is sorted
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

## 633. Sum of Square Numbers
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
## 345. Reverse Vowels of a String
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
## 4. 回文字符串
https://leetcode.com/problems/valid-palindrome-ii/description/
N
需要单独写一个验证函数
```C++

```
## 5. 归并两个有序数组
https://leetcode.com/problems/merge-sorted-array/description/
```C++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int p1 = 0;
        int p2 = 0;
        vector<int> s;
        
        while(p1<m or p2<n)
        {
            if(p1 == m) s.push_back(nums2[p2++]);
            
            else if(p2 == n) s.push_back(nums1[p1++]);

            else if(nums1[p1] <= nums2[p2]) s.push_back(nums1[p1++]);

            else if(nums1[p1] > nums2[p2]) s.push_back(nums2[p2++]);
        }
        nums1 = s;
    }
};
```
## 6. 判断链表是否存在环
https://leetcode.com/problems/linked-list-cycle/submissions/
N
1.开头记得排除头节点为空或只有一个节点的情况
2.注意循环的终止条件
3.起点不能相同，否则与循环终止条件冲突
4.走得快的指针，如果没有环，会先达到nullptr,而如果它本身或者它的下一个为nullptr，就一定没有环，所以return false
```C++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(!head or !head->next) return false;
        ListNode * slow = head;
        ListNode * fast = head->next;
        
        while(slow != fast)
        {
            if(!fast or !fast->next)
                return false;
            else
            {
                slow = slow->next;
                fast = fast->next->next;
            }
        }
        return true;
    }
};
```
## 7. 最长子序列
https://leetcode.com/problems/longest-word-in-dictionary-through-deleting/description/
```C++

```
# 链表
## 1. 找出两个链表的交点
https://leetcode.com/problems/intersection-of-two-linked-lists/description/
H
1.循环的终止条件
2.当p1或p2为空，怎么把另一条路链上来很重要，已经为空时写成p1->next = headB就错了，都空了，就更没有下一个了;
```C++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        // if(!headA) return headA;
        // if(!headB) return headB;
        ListNode * p1 = headA;
        ListNode * p2 = headB;
        
        while(p1 != p2)
        {
            if(!p1) p1 = headB;
            else if(p1) p1 = p1->next;
            
            if(!p2) p2 = headA;
            else if(p2) p2 = p2->next;
            
       }
        return p1;
    }
};
```
## 2. 链表反转
https://leetcode.com/problems/reverse-linked-list/description/
N
1.反转链表就是pre current next三个节点的更新
2.注意循环退出的条件
3.return谁要想好
```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = nullptr;
        ListNode* nex;
        
        while(head)
        {
            nex = head->next;
            head->next = pre;
            pre = head;
            head = nex;
        }
        return pre;
    }
};
```
## 3. 归并两个有序的链表
https://leetcode.com/problems/merge-two-sorted-lists/submissions/
H
1.注意哨兵节点
2.注意返回谁
```C++
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode(-1);
        ListNode* pre;
        pre = dummy;
        
        while(l1 or l2)
        {
            if(!l1 and l2)
            {
                pre->next = l2;
                pre = l2;
                l2 = l2->next;
            }
            else if(l1 and !l2)
            {
                pre->next = l1;
                pre = l1;
                l1 = l1->next;
            }
            else if(l1->val <= l2->val) 
            {
                pre->next = l1;
                pre = l1;
                l1 = l1->next;
            }
            else if(l1->val > l2->val) 
            {
                pre->next = l2;
                pre = l2;
                l2 = l2->next;
            }
        }
        return dummy->next;
    }
};
```
## 4. 从有序链表中删除重复节点
https://leetcode.com/problems/remove-duplicates-from-sorted-list/submissions/
H
1.开头注意排除特殊情况
2.哨兵节点别写反 这样就错了：dummy = pre;
3.不加这一句 pre->next = nullptr; 就会导致：
Input:[1,1,2,3,3] 
Output:[1,2,3,3] 
Expected:[1,2,3] 
```C++
    ListNode* deleteDuplicates(ListNode* head) {
        if(!head or !head->next) return head;
        
        ListNode* dummy = new ListNode(-200);
        ListNode* pre;
        pre = dummy;
        //dummy->next = head;
        while(head)
        {
            if(pre->val != head->val)
            {
                pre->next = head;
                pre = head;
                head = head->next;
            }
            else if(pre->val == head->val)
            {
                head = head->next;
            }
        }
        pre->next = nullptr;
        return dummy->next;
```
## 5. 删除链表的倒数第 n 个节点
https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/
N
```C++
```
## 6. 交换链表中的相邻结点
https://leetcode.com/problems/swap-nodes-in-pairs/description/
N
```C++
```
## 7. 链表求和
https://leetcode.com/problems/add-two-numbers-ii/description/
```C++
```
## 8. 回文链表
https://leetcode.com/problems/palindrome-linked-list/submissions/
Y
速度慢 占用多 待完善
```C++
class Solution {
public:
    bool isPalindrome(ListNode* head) {
        vector<double> s;
        vector<double> c;
        ListNode* pre = nullptr;
        ListNode* nex;
        while(head)
        {
            s.push_back(head->val);
            
            nex = head->next;
            head->next = pre;
            pre = head;
            head = nex;
        }
        while(pre)
        {
            c.push_back(pre->val);
            pre = pre->next;
        }
        if(s == c) return true;
        else return false;
    }
};
```
## 9. 分隔链表
https://leetcode.com/problems/split-linked-list-in-parts/description/
N
```C++
```
## 10. 链表元素按奇偶聚集
https://leetcode.com/problems/odd-even-linked-list/description/
N 报错未解决
```C++
class Solution {
public:
    ListNode* oddEvenList(ListNode* head) {
        ListNode* d1 = new ListNode(1);
        ListNode* d2 = new ListNode(1);
        ListNode* pre1;
        ListNode* nex1;
        ListNode* pre2;
        ListNode* nex2;
        pre1 = d1;
        pre2 = d2;
        
        while(head)
        {
            if(head->val % 2 != 0) 
            {
                pre1->next = head;
                pre1 = head;
            }
            else 
            {
                pre2->next = head;
                pre2 = head;
            }
            head = head->next;
        }
        pre1->next = d2->next;
        return d1->next;
    }
};
```
# 栈与队列
## 1.
## 2.
## 3.
## 4. 用栈实现括号匹配
https://leetcode.com/problems/valid-parentheses/description/
N
```C++
class Solution {
public:
    bool isValid(string s) {
        if(s.size() == 0 or s.size() %2 != 0)
            return false;
        stack<char> store;
        //可以使用字典
        for(char i : s)
        {
            if(i=='(' or i=='{' or i=='[')
            {
                store.push(i);
            }
            
        }
    }
};
```
