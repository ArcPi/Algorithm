#### 描述：
Given a binary tree, determine if it is height-balanced.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

#### 思路：
用两个递归，一个递归找出树的最大深度，用另一个递归判断是否是平衡二叉树
####C++代码：
```c
class Solution {
public:
    bool isBalanced(TreeNode *root) {
        if (root == NULL) { return true; }
        if (abs(maxDepth(root->left) - maxDepth(root->right)) > 1) {
            return false;
        }
        return isBalanced(root->left) and isBalanced(root->right);
 
    }
 
    int maxDepth(TreeNode *root) {
        if (root == NULL) { return 0; }
        return max(maxDepth(root->left), maxDepth(root->right)) + 1;
    }
};
```