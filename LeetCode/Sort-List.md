---
title: Sort-List
date: 2018-12-03 20:33:05
categories: LeetCode
tags: [Merge Sort, List]
---

### C++:采用归并排序的方法

#### 思路：

采用归并排序，首先要找到List的中间节点，然后一刀切开，分成L1，L2，然后递归即可。关键是怎么找到中间节点，我们设俩指针，slow，fast，slow滑动的步幅为一，fast滑动的步幅为二，这样，fast到末尾之后，slow指向中间节点。

<!-- more -->

#### 代码：

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
    ListNode *sortList(ListNode *head) {
        if(head == NULL || head->next == NULL)
            return head;
        ListNode* prev = head;
        ListNode* slow = head;
        ListNode* fast = head;
        while(fast && fast->next)
        {
            prev = slow;
            slow = slow->next;
            fast = fast->next->next;
        }
        prev->next = NULL;
        ListNode* L1 = sortList(head);
        ListNode* L2 = sortList(slow);
        return merge(L1,L2);
    }
    ListNode* merge(ListNode* L1, ListNode* L2)
    {
        ListNode* L = new ListNode(0);
        ListNode* p = L;
        while(L1 && L2)
        {
            if(L1->val val)
            {
                p->next = L1;
                L1 = L1->next;
            }
            else
            {
                p->next = L2;
                L2 = L2->next;
            }
            p = p->next;
        }
        if(L1)
        {
            p->next = L1;
        }
        if(L2)
        {
            p->next = L2;
        }
        return L->next;
    }
};
```