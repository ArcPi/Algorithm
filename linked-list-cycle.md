---
title: linked-list-cycle
date: 2018-12-04 21:41:52
categories: LeetCode
tags: [List]
---

#### 描述：

Given a linked list, determine if it has a cycle in it.

Follow up:
Can you solve it without using extra space?

#### 思路：

想想两个人跑步，一个跑的慢，一个跑的快，跑的快的最终会追上跑得慢的。这里为什么用fast->next->next 而不用fast->next->next->next ?  考虑到链表结构，所以跑步的路程是离散的。fast比slow快一格，可以保证他俩在某刻一定在一个格子里；快两格，也许fast就直接超过slow，这样就不能保证他俩在一个格子里，也就没法判定链表是否有环路。

<!--more-->

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
    bool hasCycle(ListNode *head) {
        
        if(!head || !head -> next)
            return false;
        
        ListNode* slow = head;
        ListNode* fast = head;
        
        while(fast && fast->next)
        {
            fast = fast->next->next;
            slow = slow->next;
            if(fast == slow)
                return true;
        }
        
        return false;
    }
};
```

