#### 参考：
链接：[https://www.cnblogs.com/yuzhangcmu/p/4172855.html](https://www.cnblogs.com/yuzhangcmu/p/4172855.html)
[https://zxi.mytechroad.com/blog/tree/leetcode-124-binary-tree-maximum-path-sum/](https://zxi.mytechroad.com/blog/tree/leetcode-124-binary-tree-maximum-path-sum/)
#### 描述：
题目描述

Given a binary tree, find the maximum path sum.

The path may start and end at any node in the tree.

For example:
Given the below binary tree,

       1
      / \
     2   3

Return6.

#### 思路：
看图：
![在这里插入图片描述](http://upload-images.jianshu.io/upload_images/10118984-e6dad31de7135a9e?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
计算树的最长path有2种情况：
```
1. 通过根的path.

  (1)如果左子树从左树根到任何一个Node的path大于零，可以链到root上

  (2)如果右子树从右树根到任何一个Node的path大于零，可以链到root上

2. 不通过根的path. 这个可以取左子树及右子树的path的最大值。
```
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
    int maxPathSum(TreeNode *root) {
        if(root == NULL)
            return 0;
        int ans = INT_MIN;
        maxPathDown(root, ans);
        return ans;
    }
    int maxPathDown(TreeNode* root, int& ans)
    {
        if(root == NULL)
            return 0;
        int left = max(0, maxPathDown(root->left, ans));
        int right = max(0, maxPathDown(root->right, ans));
        int sum = left + right + root->val;
        ans = max(sum, ans);
        
        return max(left, right) + root->val;
    }
};
```
```java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    int ans = Integer.MIN_VALUE;
    public int maxPathSum(TreeNode root) {
        if(root == null)
            return 0;
        maxPathDown(root);
        return ans;
    }
    
    private int maxPathDown(TreeNode root){
        if(root == null)
            return 0;
        int left = Math.max(maxPathDown(root.left), 0);
        int right = Math.max(maxPathDown(root.right), 0);
        int sum = left + right + root.val;
        ans = Math.max(ans, sum);
        
        return Math.max(left, right) + root.val;
    }
}
```
