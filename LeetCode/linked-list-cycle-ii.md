---
title: linked-list-cycle-ii
date: 2018-12-06 23:32:52
categories: LeetCode
tags: [List]
---

#### 思路：

这个说的挺好的[链接](https://www.nowcoder.com/questionTerminal/6e630519bf86480296d0f1c868d425ad)

#### 代码：

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
    ListNode *detectCycle(ListNode *head) {
        
        ListNode* slow = head;
        ListNode* fast = head;
        
        ListNode* start = head;
        ListNode* meet;
        while(fast != NULL && fast->next != NULL)
        {
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow)
            {
                meet = fast;
                break;
            }
        }
        
        if(fast == NULL || fast->next == NULL)
        {
            return NULL;
        }
        
        while(start != meet)
        {
            start = start->next;
            meet = meet->next;
        }
        
        return meet;
        
    }
};
```

