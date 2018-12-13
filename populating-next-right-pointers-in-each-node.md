#### 描述：
Given a binary tree

    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set toNULL.

Initially, all next pointers are set toNULL.

Note:

You may only use constant extra space.
You may assume that it is a perfect binary tree (ie, all leaves are at the same level, and every parent has two children).

For example,
Given the following perfect binary tree,

         1
       /  \
      2    3
     / \  / \
    4  5  6  7

After calling your function, the tree should look like:

         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL

#### 思路：
采用层次遍历的思想，采用队列，如果需要确定层次，需要另外的辅助指针。
Now:当前遍历的节点
Last：这层最后的节点
怎么能找到每一层的最后节点呢？需要nLast指针，每次更新为新加入队列的指针。想一下，当Now指针指向Last时，nLast就更新为了下一层最后一个节点。
#### C++代码：
```c
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
class Solution {
public:
    void connect(TreeLinkNode *root) {
        
        //如果树为空
        if(root == NULL)
            return;
        //定义辅助指针
        TreeLinkNode* last = root;
        TreeLinkNode* nLast = NULL;
        TreeLinkNode* now = root;
        
        queue<TreeLinkNode*> qu;
        vector<TreeLinkNode*> ve;
        qu.push(now);
        
        while(qu.size() != 0)
        {
            now = qu.front();
            ve.push_back(now);
            qu.pop();
            if(now->left != NULL)
            {
                qu.push(now->left);
                nLast = now->left;
            }
            if(now->right != NULL)
            {
                qu.push(now->right);
                nLast = now->right;
            }
            
            //遍历到最后节点，按照层顺序连接起来
            if(now == last)
            {
                for(int i = 0;i<ve.size()-1;i++)
                {
                    ve[i]->next = ve[i+1];
                }
                ve.clear();
                last = nLast;
            }
        }
    }
};
```
#### Java代码：
```Java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
import java.util.LinkedList;
import java.util.Queue;
import java.util.ArrayList;
public class Solution {
    public void connect(TreeLinkNode root) {
        if(root == null)
            return;
        
        TreeLinkNode now = root;
        TreeLinkNode last = root;
        TreeLinkNode nlast = null;
        
        Queue<TreeLinkNode> qu = new LinkedList<TreeLinkNode>();
        ArrayList<TreeLinkNode> list = new ArrayList<>();
        qu.add(now);
        
        while(qu.peek() != null)
        {
            now = qu.poll();
            list.add(now);
            if(now.left != null)
            {
                qu.add(now.left);
                nlast = now.left;
            }
            if(now.right != null)
            {
                qu.add(now.right);
                nlast = now.right;
            }
            if(now == last)
            {
                for(int i = 0; i<list.size()-1;i++)
                {
                    list.get(i).next = list.get(i+1);
                }
                list.clear();
                last = nlast;
            }
        }
    }
}
```