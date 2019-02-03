#### 描述：
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree is symmetric:
```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```
But the following is not:
```
    1
   / \
  2   2
   \   \
   3    3
```

#### 方法：
利用递归解决

#### C++代码：
```c
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
    bool isSymmetric(TreeNode *root) {
        if(!root)
            return true;
        return helper(root->left, root->right);
    }
    
    bool helper(TreeNode* left, TreeNode* right)
    {
        if(!left && !right)
            return true;
        if((left && !right) || (!left && right))
            return false;
        return left->val == right->val && helper(left->right, right->left) && helper(left->left, right->right);
    }
};
```