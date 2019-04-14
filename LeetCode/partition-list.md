# 题目描述
Given a linked list and a value x, partition it such that all nodes less than x come before nodes greater than or equal to x.

You should preserve the original relative order of the nodes in each of the two partitions.

For example,
Given1->4->3->2->5->2and x = 3,
return1->2->2->4->3->5.

# 思路
搞成俩链表，然后再合起来

# 代码
```c
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
    ListNode *partition(ListNode *head, int x) {
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        ListNode *dummyLess = new ListNode(0);
        ListNode *dummyGreater = new ListNode(0);
        
        ListNode *tmp = dummy->next;
        
        
        ListNode *tmpLess = dummyLess;
        ListNode *tmpGreater = dummyGreater;
        ListNode *tmpNext = tmp->next;
        while(tmp)
        {
            if(tmp->val < x)
            {
                tmpLess->next = tmp;
                tmpLess = tmpLess->next;
            }
            else
            {
                tmpGreater->next = tmp;
                tmpGreater = tmpGreater->next;
            }
            tmp->next = nullptr;
            tmp = tmpNext;
            tmpNext = tmpNext->next;
        }
        
        tmpLess->next = dummyGreater->next;
        
        return dummyLess->next;
        
    }
};
```