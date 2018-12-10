#### 描述：
Given a binary tree containing digits from0-9only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path1->2->3which represents the number123.

Find the total sum of all root-to-leaf numbers.

For example,
```

    1
   / \
  2   3
```

The root-to-leaf path1->2represents the number12.
The root-to-leaf path1->3represents the number13.

Return the sum = 12 + 13 =25.

#### 方法：
采用根左右的遍历方式，每一层：上一层之和*10 + 这层的值。

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
    int preOrderTravel(TreeNode* root, int sum)
    {
        if(root == NULL)
            return 0;
        sum = sum * 10 + root->val;
        if(root->left == NULL && root->right == NULL)
            return sum;
        return preOrderTravel(root->left,sum) + preOrderTravel(root->right, sum);
    }
    int sumNumbers(TreeNode *root) {
        int sum = 0;
        if(root == NULL)
            return 0;
        return preOrderTravel(root, sum);
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
    public int preOrderTravel(TreeNode root, int sum){
        if(root == null)
            return 0;
        sum = sum*10 + root.val;
        if(root.left == null && root.right == null)
            return sum;
        return preOrderTravel(root.left, sum) + preOrderTravel(root.right, sum);
    }
    public int sumNumbers(TreeNode root) {
        int sum = 0;
        if(root == null)
            return 0;
        return preOrderTravel(root, sum);
    }
}
```

