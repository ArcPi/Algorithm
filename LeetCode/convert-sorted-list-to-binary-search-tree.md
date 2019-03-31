# 题目描述
Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

# 思想
找出中间节点，然后断开，构造出二分查找树

# 代码一
对于中间节点的处理：直接令成nullptr
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode *sortedListToBST(ListNode *head) {
		if (head == nullptr)
			return nullptr;
		if (head->next == nullptr)
			return new TreeNode(head->val);
		ListNode *preMid = nullptr;
		ListNode *mid = head;
        ListNode *end = head;
        while(end != nullptr && end->next != nullptr)
        {
            preMid = mid;
            mid = mid->next;
            end = end->next->next;
        }
		TreeNode *root = new TreeNode(mid->val);
		preMid->next = nullptr;

		root->left = sortedListToBST(head);
		root->right = sortedListToBST(mid->next);

		return root;
	}
};
```

# 代码二
对于中间节点的处理：记录下来。换句话说，不令成nullptr，知道是中间节点即可
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode *sortedListToBST(ListNode *head) {
        return makeBST(head, nullptr);
    }
    
    TreeNode *makeBST(ListNode *head, ListNode *end){
        if(head == end)
            return nullptr;
        ListNode *mid = head;
        ListNode *fast = head;
        while(fast != end && fast->next != end){
            mid = mid->next;
            fast = fast->next->next;
        }
        TreeNode *root = new TreeNode(mid->val);
        root->left = makeBST(head, mid);
        root->right = makeBST(mid->next, end);
        
        return root;
    }
};
```
