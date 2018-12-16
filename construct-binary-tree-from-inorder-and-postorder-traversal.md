#### 描述：
Given inorder and postorder traversal of a tree, construct the binary tree.

Note: 
You may assume that duplicates do not exist in the tree.

#### 思想：
就按照中序遍历和后序遍历建立二叉树

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
    TreeNode *buildTree(vector<int> &inorder, vector<int> &postorder) {
        if(inorder.size() == 0)
            return NULL;
        int size = postorder.size();
        TreeNode* root = new TreeNode(postorder[size-1]);
        postorder.erase(postorder.end()-1);
        if(postorder.size() == 0)
            return root;
        vector<int>::iterator result = find(inorder.begin(),inorder.end(),postorder[size-1]);
        vector<int> inleft,inright,postleft,postright;
        inleft.assign(inorder.begin(),result);
        inright.assign(result+1, inorder.end());
        postleft.assign(postorder.begin(), postorder.begin()+inleft.size());
        postright.assign(postorder.begin()+inleft.size(), postorder.end());
        
        root->left = buildTree(inleft, postleft);
        root->right = buildTree(inright, postright);
        
        return root;
        
    }
};
```