#### 描述：
Given a binary tree and a sum, find all root-to-leaf paths where each path's sum equals the given sum.

```
For example:
Given the below binary tree andsum = 22,
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1
return

[
   [5,4,11,2],
   [5,8,4,5]
]
```
####思路：
这个题和上一题差不多，关键就是怎么处理存储的过成，看到大佬充分利用传值和传引用把这道题解决了，牛逼。

####C++代码：
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
    vector<vector<int> > pathSum(TreeNode *root, int sum) {
        vector<vector<int>> res;
        vector<int> tmp;
        find(root,res,tmp,sum);
        
        return res;
    }
    
    void find(TreeNode* root, vector<vector<int>> &res, vector<int> tmp,int sum)
    {
        if(root == NULL)
            return;
        tmp.push_back(root->val);
        if(root->left==NULL && root->right ==NULL && root->val ==sum)
        {
            res.push_back(tmp);
        }
        
        find(root->left,res,tmp,sum-root->val);
        find(root->right,res,tmp,sum-root->val);
    }
};
```

#### Java代码：
```Java
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
import java.util.*;
public class Solution {
    
    public ArrayList<ArrayList<Integer>> pathSum(TreeNode root, int sum) {
        ArrayList<ArrayList<Integer> > res = new ArrayList<>();
        ArrayList<Integer> tmp = new ArrayList<>();
        find(root,res,tmp,sum);
        
        return res;
    }
    
    public void find(TreeNode root, ArrayList<ArrayList<Integer> > res,ArrayList<Integer> tmp,int sum){
        if(root == null)
            return ;
        tmp.add(root.val);
        if(root.left==null && root.right==null && root.val == sum){
            res.add(tmp);
        }
        find(root.left, res, new ArrayList<Integer>(tmp), sum-root.val);
        find(root.right, res, new ArrayList<Integer>(tmp), sum-root.val);
    }
}
```

