# 题目描述
```c++
You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
```
# 思路
设置以下变量：
num：记录链表节点值，进位到当前位值的和
carry：记录进位
**按顺序有以下几种情况**
##1 两链表分别不为空
num = L1->val + L2->val + carry
carry = num/10
##2 仅剩一个链表不为空
num = L->val + carry
carry = num/10
##3 carry的值大于0
# 代码
```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *addTwoNumbers(ListNode *l1, ListNode *l2) {
        int num = 0;
        int carry = 0;
        ListNode *tmp1 = l1;
        ListNode *tmp2 = l2;
        ListNode *dummy = new ListNode(0);
        ListNode *ptr = dummy;
        
        while(tmp1 && tmp2)
        {
            num = tmp1->val + tmp2->val + carry;
            carry = num/10;
            ListNode *newNode = new ListNode(num % 10);
            ptr->next = newNode;
            ptr = ptr->next;
            num = 0;
            
            tmp1 = tmp1->next;
            tmp2 = tmp2->next;
        }
        while(tmp1)
        {
            num = tmp1->val + carry;
            carry = num/10;
            ListNode *newNode = new ListNode(num%10);
            ptr->next = newNode;
            ptr = ptr->next;
            num = 0;
            
            tmp1 = tmp1->next;
            
        }
         while(tmp2)
        {
            num = tmp2->val + carry;
            carry = num/10;
            ListNode *newNode = new ListNode(num%10);
            ptr->next = newNode;
            ptr = ptr->next;
            num = 0;
            
            tmp2 = tmp2->next;
        }
        if(carry > 0)
        {
            ListNode *newNode = new ListNode(carry);
            ptr->next = newNode;
            ptr = ptr->next;
        }
        
        return dummy->next;
    }
};
```