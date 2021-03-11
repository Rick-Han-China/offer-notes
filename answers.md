# 3.数组中重复的数字
https://www.nowcoder.com/practice/623a5ac0ea5b4e5f95552655361ae0a8?tpId=13&tqId=11203&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
Y
```C++
    public:
    bool duplicate(int numbers[], int length, int* duplication) 
    {
        if(length<=1) // 数组长度不大于1，一定没有重复数字
            return false;
        //采用对号入座方法，把数组中值等于i的数字放到第i个位置上
        for(int i=0;i<length;i++) // 遍历每个数字
        {
            if(i == numbers[i]); // 如果第i个数字的值和i相等，表示无需进行放置，略过。
            
            else if(numbers[i] == numbers[numbers[i]]) // 如果i位置上的数字和它该去的位置上的数字相等，找到重复数字
            {
                duplication[0] = numbers[i];
                return true;
            }
            
            else // 当上述相等条件都不满足，交换位置，把当前数字放到它对应的位置上去
                swap(numbers[i], numbers[numbers[i]]);
        }
        
        return false; // 循环退出，说明不存在重复数字
    }
};
```
# 4.二维数组中的查找
https://www.nowcoder.com/practice/abc3fe2ce8e146608e868a70efebf62e?tpId=13&tqId=11154&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
Y
```C++
class Solution {
public:
    bool Find(int target, vector<vector<int> > array) {
        int cl = array[0].size();
        int li = array.size();
        if(li == 0 or cl == 0) // 排除数组为空的情况
            return false;
        
        int i = 0;
        int j = cl - 1; // 定义数组索引
        
        //总体思路是从矩阵的右上角向左下角查找，每次排除一行或一列的数字    
        while(i <= li-1 and j >= 0) // 当k不超出数组范围就进行循环判断
        {
            if(array[i][j]==target)
                return true;
            else if(array[i][j]>target)
                j--;
            else if(array[i][j]<target)
                i++;
        }
        return false;
    }
};
```
# 5.替换空格
https://www.nowcoder.com/practice/4060ac7e3e404ad1a894ef3e17650423?tpId=13&tqId=11155&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
Y
```C++
class Solution {
public:
	void replaceSpace(char *str,int length) {
        if(length == 0)
            return; // 养成排除空数组的习惯
        int p1 = 0;
        int p2 = length-1;
        
        for(p1;p1<length;p1++)
        {
            if(str[p1] == ' ')
                p2 = p2 + 2;
        }
        p1--; // 比较关键的一步，因为此时的p1=length,会导致下边的循环越界
        for(p1;p1>=0;p1--)
        {
            if(str[p1] != ' ')
                str[p2--] = str[p1];
            else
            {
                str[p2--] = '0';
                str[p2--] = '2';
                str[p2--] = '%';
            }
        }
	}
};
```
# 42. 和为S的两个数字
https://www.nowcoder.com/practice/390da4f7a00f44bea7c2f3d19491311b?tpId=13&tqId=11195&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
Y
```C++
class Solution {
public:
    vector<int> FindNumbersWithSum(vector<int> array,int sum) {
        int p1 = 0;
        int p2 = array.size() - 1;
        vector<int> li;
        
        while(p1<p2)
        {
            if((array[p1] + array[p2]) == sum)
            {
                li.push_back(array[p1]);
                li.push_back(array[p2]);
                return li;
            }
            else if((array[p1] + array[p2]) < sum)
               p1++;
            else if((array[p1] + array[p2]) > sum)
               p2--;
        }
        return li; //注意这里的return，C++不像python可以直接写 return[p1,p2],得自己先创建个符合输出要求的数据结构
     }
 };
 ```
# 6.从尾到头打印链表
https://www.nowcoder.com/practice/d0267f7f55b3412ba93bd35cfa8e8035?tpId=13&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
Y
```C++
第一种：
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> li;
        ListNode * p = head;
        
        while(p)
        {
            li.push_back(p->val);
            p = p->next;
        }
        return vector<int>(li.rbegin(), li.rend()); //这里的输出比较有特点
    }
};

第二种：和前一种方法功能一样，只是使用的函数不同
 vector<int> str;
        
        while(head)
        {
            str.push_back(head->val);//这里为什么把->换成 . 不对
            head = head->next;
        }
        std:reverse(str.begin(), str.end());
        
        return str;

第三种：递归法-未完善，觉得小题大做

第四种：改变指针指向
/*
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> al;
        ListNode* pre = nullptr;
        ListNode* next;
        while(head)
        {
            next = head->next; // 提前存储下一个节点
            head->next = pre; // 指针指向前一个
            pre = head; // 用过的节点变成前一个节点
            head = next; // 让下一个节点变成当前节点
        }
        
        while(pre)
        {
            al.push_back(pre->val);
            pre = pre->next;
        }
        return al;
    }
};

第五种：使用stack，自然形成逆序
```
# 58.1翻转单词顺序列
https://www.nowcoder.com/practice/3194a4f4cf814f63919d0790578d51f3?tpId=13&tqId=11197&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
N
```C++
//思路：先翻转每个单词，再翻转字符串
//注意：这题出得不好，容易让人误解，做题时很容易认为.号能作为flag，但是根据答案，会有把正常语序反转成逆语序的，正常人谁会把对的改成错的啊
class Solution {
public:
    string ReverseSentence(string str) {
        string store;
        string temp;
        int p2 = str.size() - 1;
        
        for(p2;p2>=0;p2--)
        {
            if(str[p2] != ' ')
            {
                temp = str[p2] + temp;
            }
            else if(str[p2] == ' ')
            {
                store = store + temp + ' ';
                temp = ""; //这里用单引号就错了，因为temp是string类型
            }
        }
        store = store + temp;//这行很重要，因为此时temp中可能还存放着一个单词
        return store;
    }
};
```
# 58.2 左旋转字符串
https://www.nowcoder.com/practice/12d959b108cb42b1ab72cef4d36af5ec?tpId=13&tqId=11196&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
Y
```C++
class Solution {
public:
    string LeftRotateString(string str, int n) {
        int p1 = 0;
        int p2 = str.size() - 1;
        string s1;
        string s2;
        while(p1<n)
        {
            s2.push_back(str[p1]);
            p1++;
        }
        while(p2>=n)
        {
            s1.push_back(str[n]);
            n++;
        }
        return s1+s2;
//         if (n > str.size()) return str;
//         return str.substr(n) + str.substr(0, n); 这两行是比较简介的写法
    }
};
```
# JZ15. 反转链表
https://www.nowcoder.com/practice/75e878df47f24fdc9dc3e400ec6058ca?tpId=13&tqId=11168&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
H
```C++
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* ReverseList(ListNode* pHead) {
        ListNode * pre = nullptr;
        ListNode * next;
        while(pHead)
        {
            next = pHead->next;
            pHead->next = pre; // 到这里节点已经指向前一个了
            pre = pHead;
            pHead = next; // 到这里把节点更新，循环进行
        }
        return pre; // 这里return谁得考虑清楚，其实比较简单，只有当前节点，也就是此时的pHead为空时，循环
                    // 才能退出，所以返回pre才对
    }
};
```
# 合并有序链表
https://www.nowcoder.com/practice/d8b6b4358f774294a89de2a6ac4d9337?tpId=13&tqId=11169&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
迭代方法
H
```C++
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2) {
        ListNode * dummy =new ListNode(0); //设置哨兵，注意new
        ListNode * cur = dummy;
        
        while(pHead1 and pHead2)
        {
            if(pHead1->val <= pHead2->val)
            {
                cur->next = pHead1;
                pHead1 = pHead1->next;
            }
            else if(pHead1->val > pHead2->val)
            {
                cur->next = pHead2;
                pHead2 = pHead2->next;
            }
            cur = cur->next;
        }
        if(pHead1) cur->next = pHead1;
        else cur->next = pHead2; //这两步判断很重要，要把剩下的链上来
        return dummy->next;
    }
};
```
递归方法，递归方法的关键在于 1.明白递归终止的条件 2.递归函数返回值的含义 3.递归函数一定是缩小递归区间的，下一步的递归区间是什么？
N
```C++
class Solution {
public:
    ListNode* Merge(ListNode* pHead1, ListNode* pHead2) {
     if (!pHead1) return pHead2;
     if (!pHead2) return pHead1;
     if (pHead1->val <= pHead2->val)
     {
           pHead1->next = Merge(pHead1->next, pHead2);
           return pHead1;
     }
     else
     {
         pHead2->next = Merge(pHead1, pHead2->next);
         return pHead2;
     }
    }
};
```
# 链表中倒数第K个节点
https://www.nowcoder.com/practice/529d3ae5a407492994ad2a246518148a?tpId=13&tqId=11167&tPage=1&rp=1&ru=%2Fta%2Fcoding-interviews&qru=%2Fta%2Fcoding-interviews%2Fquestion-ranking&from=cyc_github&tab=answerKey
N
编译未通过，正在排查
```C++
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* FindKthToTail(ListNode* pListHead, unsigned int k) {
        ListNode * pre = nullptr;
        ListNode * next;
        ListNode * store;
        
        unsigned int i = 1;
        
        while(pListHead)
        {
            next = pListHead -> next;
            pListHead -> next = pre;
            pre = pListHead;
            pListHead = next;
        }
        
        while(i!=k)
        {
            pre = pre -> next;
            i++;
        }
        return pre;
    }
};
```
# 18.2 删除链表中重复的节点
关键在于，通过while处理那些无法确定连续相等长度的节点
```C++
/*
struct ListNode {
    int val;
    struct ListNode *next;
    ListNode(int x) :
        val(x), next(NULL) {
    }
};
*/
class Solution {
public:
    ListNode* deleteDuplication(ListNode* phead) {
        ListNode * dummy = new ListNode(-1);
        ListNode * pre = dummy;
        ListNode * cur = phead;
        pre->next = cur;
        while(cur)
        {
            if(cur->next and cur->val == cur->next->val)
            {
                cur = cur->next;
                while(cur->next and cur->val == cur->next->val)
                {
                    cur = cur->next;
                }
                cur = cur->next;
                pre->next = cur;
            }
            else
            {
                pre = cur;
                cur = cur->next;
            }
        }
        return dummy->next;
    }
};
```
# 52. 两个链表的第一个公共节点
巧妙的地方在于：空节点也是某种意义上的公共节点
这道题要注意判断条件：应判断自身是否为空，而不是下一个节点是否为空，否则就无法进入都为空的状态，也就无法跳出循环了
```C++
/*
struct ListNode {
	int val;
	struct ListNode *next;
	ListNode(int x) :
			val(x), next(NULL) {
	}
};*/
class Solution {
public:
    ListNode* FindFirstCommonNode( ListNode* phead1, ListNode* phead2) {
        ListNode * p1 = phead1;
        ListNode * p2 = phead2;
        while(phead1 != phead2)
        {
            if(phead1) phead1 = phead1->next;
            else if(!phead1) phead1 = p2;
            if(phead2) phead2 = phead2->next;
            else if(!phead2) phead2 = p1;
        }
        return phead1;
    }
};
```
