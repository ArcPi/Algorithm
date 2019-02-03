---
title: reorder-list
date: 2018-12-04 10:40:55
categories: LeetCode
tags: [List]
---

#### 题目描述：

Given a singly linked list *L*: *L* 0→*L* 1→…→*L* *n*-1→*L* n,
reorder it to: *L* 0→*L* *n* →*L* 1→*L* *n*-1→*L* 2→*L* *n*-2→…

You must do this in-place without altering the nodes' values.

For example,
Given{1,2,3,4}, reorder it to{1,4,2,3}.

<!--more-->

#### 思路一：

这是一个单链表，按照题目描述，我们没法从后往前找链表元素，为了实现这个目的，我们可以设置一个stack，这样就可以记录从后往前的信息了。

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
    void reorderList(ListNode *head) {
        if(!head || !head->next)
            return;
        
        ListNode* dummy = new ListNode(0);
        ListNode* rear = head;
        stack<ListNode*> st;
        
        while(rear)
        {
            st.push(rear);
            rear = rear->next;
        }
        
        rear = st.top();
        st.pop();
        
        ListNode* headnext = head->next;
        ListNode* p = dummy;
        
        while(head->next != rear && head != rear)
        {
            headnext = head->next;
            head->next = rear;
            rear->next = NULL;
            p->next = head;
            p = p->next->next;
            
            head = headnext;
            rear = st.top();
            st.pop();
        }
        if(head == rear)
        {
            rear->next = NULL;
            p->next = rear;
        }
        if(head->next == rear)
        {
            head->next = rear;
            rear->next = NULL;
            p->next = head;
        }
        
        head = dummy->next;
    }     
};
```

#### 思路二：

找到链表中间节点，将链表分为链表一，链表二；采用头插法逆序链表二；合并链表一链表二。

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
    void reorderList(ListNode *head) {
        
        //链表为空或者只有一个元素，不需要进行操作
        //（其实只有俩元素也不需要操作，可以合并到下边情况）
        if(!head || !head->next)
            return;
        
        //找到中间节点，拆分链表为链表一，链表二
        ListNode* slow = head;
        ListNode* fast = head;
        ListNode* preslow;
        while(fast && fast->next)
        {
            preslow = slow;
            slow = slow->next;
            fast = fast->next->next;
        }
        preslow->next = NULL;
        
        //采用头插法，将链表二逆序
        ListNode* dummy = new ListNode(0);
        while(slow)
        {
            ListNode* slownext = slow->next;
            slow->next = dummy->next;
            dummy->next = slow;
            slow = slownext;
        }
        
        //将链表一链表二合并
        ListNode* firstList = head;
        ListNode* secondList = dummy->next;
        ListNode* firstListnext;
        ListNode* secondListnext;
        
        ListNode* p = dummy;
        while(firstList && secondList)
        {
            firstListnext = firstList->next;
            secondListnext = secondList->next;
            
            firstList->next = NULL;
            secondList->next = NULL;
            
            firstList->next = secondList;
            p->next = firstList;
            
            p = p->next->next;
            firstList = firstListnext;
            secondList = secondListnext;
        }
        
        //这段if可以不要
        //因为按照我们划分，链表二元素个数总是大于等于链表一元素个数
        if(firstList)
        {
            firstList->next = NULL;
            p->next = firstList;
        }
        if(secondList)
        {
            secondList->next = NULL;
            p->next = secondList;
        }
        
        head = dummy->next;
    }
};
```

