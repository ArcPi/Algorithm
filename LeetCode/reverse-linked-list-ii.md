# 题目描述：
Reverse a linked list from position m to n. Do it in-place and in one-pass.

For example:
Given1->2->3->4->5->NULL, m = 2 and n = 4,

return1->4->3->2->5->NULL.
# 注意事项
一定要找到m,n的位置之后再断链，要不会出问题
# 代码
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
    ListNode *reverseBetween(ListNode *head, int m, int n) {
        if(head == nullptr)
            return head;
        if(m == n)
            return head;
        // 添加头节点
        ListNode tmpnode(0);
        ListNode *prehead = &tmpnode;
        prehead->next = head;
        
        // 找到m节点以及其前边的节点
        ListNode *mPosi = prehead;
        ListNode *prePosi = prehead;
        while(m--)
        {
            prePosi = mPosi;
            mPosi = mPosi->next;
        }
        
        // 找到n节点以及后边节点
        ListNode *nPosi = prehead;
        ListNode *postPosi = nullptr;
        while(n--)
        {
            nPosi = nPosi->next;
        }
        postPosi = nPosi->next;
        
        //进行断链操作
        prePosi->next = nullptr;
        nPosi->next = nullptr;
        
        //重新组织顺序
        ListNode *tmp = mPosi;
        ListNode *tmpnext = mPosi->next;
        while(tmp)
        {
            tmp->next = prePosi->next;
            prePosi->next = tmp;
            tmp = tmpnext;
            tmpnext = tmpnext->next;
        }
        
        //合并链
        mPosi->next = postPosi;
        
        return prehead->next;
        
    }
};
```