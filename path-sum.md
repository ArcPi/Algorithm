#### 描述：
Given a binary tree and a sum, determine if the tree has a root-to-leaf path such that adding up all the values along the path equals the given sum.
```
For example:
Given the below binary tree andsum = 22,
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \      \
        7    2      1
return true, as there exist a root-to-leaf path5->4->11->2which sum is 22.
```
这个题的题意时从叶节点到根节点有没有一条和为sum的路径，若有，返回true，没有返回false。一开始理解错了题意，一直做不出。
#### 思路：
用递归可以解得
####C++代码：
```c

class Solution {
public:
    bool hasPathSum(TreeNode *root, int sum) {
       if(root == NULL)
           return false;
        if(root->left == NULL && root->right == NULL && sum - root->val == 0)
           return true;
        return hasPathSum(root->left,sum-root->val) || hasPathSum(root->right,sum-root->val);
    }
};
```
#### Java代码：
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
    
    public boolean hasPathSum(TreeNode root, int sum) {
        if(root == null)
            return false;
        if(root.left==null && root.right==null && root.val==sum)
            return true;
        return hasPathSum(root.left, sum - root.val) || hasPathSum(root.right, sum - root.val);
        
    }
}
```