#### 描述：
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree{3,9,20,#,#,15,7},
```
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:
```
[
  [3],
  [20,9],
  [15,7]
]
```
#### 方法：
普通的层次遍历方法，在最后边加一个奇偶层的判断，奇数层就倒序（层数从零开始计数）
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
    vector<vector<int> > zigzagLevelOrder(TreeNode *root) {
        vector<vector<int> > res;
        vector<int> store;
        if(root == NULL)
            return res;
        
        queue<TreeNode* > qu;
        TreeNode* last = root;
        TreeNode* nlast = NULL;
        qu.push(root);
        while(qu.size())
        {
            TreeNode* tmp = qu.front();
            store.push_back(tmp->val);
            qu.pop();
            if(tmp->left)
            {
                qu.push(tmp->left);
                nlast = tmp->left;
            }
            if(tmp->right)
            {
                qu.push(tmp->right);
                nlast = tmp->right;
            }
            if(tmp == last)
            {
                last = nlast;
                res.push_back(store);
                store.clear();
            }
        }
        
        for(int i = 0; i<res.size();i++)
        {
            if(i%2 == 1)
            {
                reverse(res[i].begin(),res[i].end());
            }
        }
        
        return res;
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
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;
import java.util.Collections;
public class Solution {
    public ArrayList<ArrayList<Integer>> zigzagLevelOrder(TreeNode root) {
       
        ArrayList<ArrayList<Integer>> res = new ArrayList<ArrayList<Integer>>();
         if(root == null)
            return res;
        ArrayList<Integer> store = new ArrayList<Integer>();
        Queue<TreeNode> queue = new LinkedList<>();
        TreeNode last = root;
        TreeNode nlast = null;
        
        queue.add(root);
        
        while(queue.peek() != null){
            TreeNode tmp = queue.poll();
            store.add(tmp.val);
            
            if(tmp.left != null){
                nlast = tmp.left;
                queue.add(tmp.left);
            }
            if(tmp.right != null){
                nlast = tmp.right;
                queue.add(tmp.right);
            }
            if(tmp == last){
                last = nlast;
                res.add(new ArrayList<Integer>(store));
                store.clear();
            }
        }
        
        for(int i = 0; i<res.size(); i++){
            if(i%2 == 1){
                Collections.reverse(res.get(i));
            }
        }
        
        return res;
    }
}
```