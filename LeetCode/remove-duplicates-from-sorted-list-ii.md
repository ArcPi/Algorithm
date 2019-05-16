# 题目描述
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only distinct numbers from the original list.

For example,
Given1->2->3->3->4->4->5, return1->2->5.
Given1->1->1->2->3, return2->3.

# 思路
可以用递归来做，思路简洁。链表无非分为两种状态，当前节点与下一节点 相同 或不同。不同，直接递归；相同，处理后递归。

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
    ListNode *deleteDuplicates(ListNode *head) 
    {
        if (!head || !head->next)
            return head;
        if (head->val != head->next->val)
        {
            head->next = deleteDuplicates(head->next);
            return head;
        }
        else
        {
            int tmp = head->val;
            while (head->val==tmp)
            {
                head = head->next;
                if (!head)
                    return NULL;
            }
            return deleteDuplicates(head);
        }
    }
};

```