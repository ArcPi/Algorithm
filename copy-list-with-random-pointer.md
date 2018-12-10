---
title: copy-list-with-random-pointer
date: 2018-12-09 00:27:33
categories: LeetCode
tags: [List]
---

#### 描述：

A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a deep copy of the list.

<!--more-->

#### 思想：

[参考这个链接](https://blog.csdn.net/ljiabin/article/details/39054999)

#### C++代码

```c
/**
 * Definition for singly-linked list with a random pointer.
 * struct RandomListNode {
 *     int label;
 *     RandomListNode *next, *random;
 *     RandomListNode(int x) : label(x), next(NULL), random(NULL) {}
 * };
 */
class Solution {
public:
    RandomListNode *copyRandomList(RandomListNode *head) {
        if(head == NULL) return head;
        
        //第一遍扫描，把复制出来的新节点插在原节点之后
        RandomListNode* node = head;
        while(node != NULL)
        {
            RandomListNode* tmp = new RandomListNode(node->label);
            tmp->next = node->next;
            node->next = tmp;
            node = node->next->next;
        }
        
        //第二遍扫描，根据原节点的random，给新节点的random赋值
        node = head;
        while(node!=NULL)
        {
            if(node->random != NULL) node->next->random = node->random->next;
            node = node->next->next;//肯定是偶数个，并且node都指在奇数位置，所以while这样判断就好
        }
        
        
        RandomListNode* newhead = head->next;
        
        //第三遍扫描，把新节点从圆脸点拆分出来
        node = head;
        while(node != NULL)
        {
            RandomListNode* tmp = node->next;
            node->next = tmp->next;
            if(tmp->next != NULL) tmp->next = tmp->next->next;
            node = node->next;
        }
        
        return newhead;
    }
};
```

#### Java代码：

```java
/**
 * Definition for singly-linked list with a random pointer.
 * class RandomListNode {
 *     int label;
 *     RandomListNode next, random;
 *     RandomListNode(int x) { this.label = x; }
 * };
 */
public class Solution {
    public RandomListNode copyRandomList(RandomListNode head) {
        if(head == null)
            return head;
        
        //在原节点后边插入新建的节点
        RandomListNode p = head;
        while(p != null){
            RandomListNode tmp = new RandomListNode(p.label);
            tmp.next = p.next;
            p.next = tmp;
            p = tmp.next;
        }
        
        //按照原节点的random顺序，建立新节点的random顺序
        p = head;
        while(p != null){
            if(p.random != null){
                p.next.random = p.random.next;
            }
            p = p.next.next;
        }
        
        //从我们新建的这个链表中，把我们需要的摘出来
        RandomListNode newnode = head.next;
        p = head;
        while(p != null){
            RandomListNode tmp = p.next;
            p.next = tmp.next;
            if(tmp.next != null)
                tmp.next = tmp.next.next;
            p = p.next;
        }
        
        return newnode;
    }
}
```



