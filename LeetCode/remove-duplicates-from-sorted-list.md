# 题目描述
Given a sorted linked list, delete all duplicates such that each element appear only once.

For example,
Given1->1->2, return1->2.
Given1->1->2->3->3, return1->2->3.

# 思路：
设置俩指针，其中一个指针探测往后的值是不是与另一个指针的值相同
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
    ListNode *deleteDuplicates(ListNode *head) {
        ListNode *tmp1 = head;
        ListNode *tmp2 = head;
        while(tmp1 != nullptr)
        {
            while(tmp2 != nullptr && tmp1->val == tmp2->val)
            {
                tmp2 = tmp2->next;
            }
            tmp1->next = tmp2;
            tmp1 = tmp1->next;
        }
        
        return head;
    }
};
```