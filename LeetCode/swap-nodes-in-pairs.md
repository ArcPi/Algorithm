# 题目描述
Given a linked list, swap every two adjacent nodes and return its head.

For example,
Given1->2->3->4, you should return the list as2->1->4->3.

Your algorithm should use only constant space. You may not modify the values in the list, only nodes itself can be changed.

# 思路
1. 设置两个指针，preFlag，postFlag分别指向两个要交换的节点的前一个位置和后一个位置
2. 交换两个节点
3. 循环此过程
4. 终止条件：postFlag && postFlag->next == 0

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
    ListNode *swapPairs(ListNode *head) {
        if(head == nullptr || head->next == nullptr)
            return head;
        ListNode *dummy = new ListNode(0);
        dummy->next = head;
        
        ListNode *preFlag = dummy;
        ListNode *pFirst = dummy->next;
        ListNode *pSecond = pFirst->next;
        ListNode *postFlag = pSecond->next;
        
        while(postFlag && postFlag->next)
        {
            preFlag->next = pSecond;
            pSecond->next = pFirst;
            pFirst->next = postFlag;
            
            preFlag = pFirst;
            pFirst = preFlag->next;
            pSecond = pFirst->next;
            postFlag = pSecond->next;
        }
        preFlag->next = pSecond;
        pSecond->next = pFirst;
        pFirst->next = postFlag;
        
        return dummy->next;
    }
};
```