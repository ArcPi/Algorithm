# 题目描述
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

# 思路
两两进行比较

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
    ListNode *mergeKLists(vector<ListNode *> &lists) {
        if(lists.size() == 0)
            return nullptr;
        if(lists.size() == 1)
            return lists[0];
        ListNode *pFirst = lists[0];
        
        for(int i = 1; i<lists.size();i++)
        {
            ListNode *pSecond = lists[i];
            ListNode *dummy = new ListNode(0);
            ListNode *ptr = dummy;
            while(pFirst && pSecond)
            {
                if(pFirst->val < pSecond->val)
                {
                    ptr->next = pFirst;
                    pFirst = pFirst->next;
                }
                else
                {
                    ptr->next = pSecond;
                    pSecond = pSecond->next;
                }
                ptr = ptr->next;
            }
            
            ListNode *rest = pFirst?pFirst:pSecond;
            if(rest)
            {
                ptr->next = rest;
            }
            pFirst = dummy->next;
            delete dummy;
        }
        
        return pFirst;
        
    }
};
```