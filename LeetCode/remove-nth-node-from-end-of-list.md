# 题目描述
```
Given a linked list, remove the n th node from the end of list and return its head.

For example,

   Given linked list: 1->2->3->4->5, and n = 2.

   After removing the second node from the end, the linked list becomes 1->2->3->5.
Note: 
Given n will always be valid.
Try to do this in one pass.


```

# 思路
设置俩指针，间隔距离为n

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
    ListNode *removeNthFromEnd(ListNode *head, int n) {
        ListNode dummytmp(0);
        ListNode *dummy = &dummytmp;
        dummy->next = head;
        
        ListNode *pEnd = dummy;
        ListNode *pLink = dummy;
        
        for(int i = 0;i<n;i++)
        {
            pEnd = pEnd->next;
        }
        while(pEnd->next)
        {
            pLink = pLink->next;
            pEnd = pEnd->next;
        }
        ListNode *tmp = pLink->next;
        pLink->next = tmp->next;
        delete tmp;
        tmp = nullptr;
        
        return dummy->next;
    }
};
```