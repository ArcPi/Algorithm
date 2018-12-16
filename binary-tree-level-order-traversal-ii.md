#### 描述：
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree{3,9,20,#,#,15,7},
```
    3
   / \
  9  20
    /  \
   15   7
```
return its bottom-up level order traversal as:
```
[
  [15,7]
  [9,20],
  [3],
]
```

confused what"{1,#,2,3}"means? > read more on how binary tree is serialized on OJ.


OJ's Binary Tree Serialization:
The serialization of a binary tree follows a level order traversal, where '#' signifies a path terminator where no node exists below.

Here's an example:
```
   1
  / \
 2   3
    /
   4
    \
     5
```
The above binary tree is serialized as"{1,2,3,#,#,4,#,#,5}".

#### 方法：
典型的层次遍历的方法

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
    vector<vector<int> > levelOrderBottom(TreeNode *root) {
        vector<vector<int>> res;
        vector<int> tmp;
        queue<TreeNode* > qu;
        TreeNode* last = root;
        TreeNode* nlast;
        qu.push(root);
        
        if(root == NULL)
            return res;
        
        while(qu.size())
        {
            TreeNode* node = qu.front();
            tmp.push_back(node->val);
            qu.pop();
            if(node->left)
            {
                nlast = node->left;
                qu.push(node->left);
            }
            if(node->right)
            {
                nlast = node->right;
                qu.push(node->right);
            }
            if(node == last)
            {
                res.push_back(tmp);
                tmp.clear();
                last = nlast;
            }
        }
        
        reverse(res.begin(),res.end());
        
        return res;
        
    }
};
```
####Java代码：
```java

import java.util.*;
public class Solution {
   public ArrayList<ArrayList<Integer>> levelOrderBottom(TreeNode root) {
        ArrayList<ArrayList<Integer>> res = new ArrayList<>();
        if(root == null) return res;
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        while ( ! queue.isEmpty()) {
            ArrayList<Integer> list = new ArrayList<>();
            int size = queue.size();
            for (int i = 0; i < size; i ++ ) {
                TreeNode temp = queue.poll();
                list.add(temp.val);
                if(temp.left != null) queue.add(temp.left);
                if(temp.right != null) queue.add(temp.right);
            }
            res.add(0,list);
        }
        return res;
    }
}

```