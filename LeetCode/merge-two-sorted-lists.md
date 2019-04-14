# 题目描述
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists
# 思路
直接链起来就好
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
    ListNode *mergeTwoLists(ListNode *l1, ListNode *l2) {
        ListNode *dummy = new ListNode(0);
        ListNode *ptr = dummy;
        while(l1 && l2)
        {
            ListNode *tmp;
            if(l1->val < l2->val)
            {
                tmp = l1;
                l1 = l1->next;
            }
            else
            {
                tmp = l2;
                l2 = l2->next;
            }
            tmp->next = ptr->next;
            ptr->next = tmp;
            ptr = ptr->next;
        }
        if(l1)
            ptr->next = l1;
        if(l2)
            ptr->next = l2;
        return dummy->next;
    }
};
```