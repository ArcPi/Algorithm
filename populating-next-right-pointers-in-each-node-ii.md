#### 描述：
Follow up for problem "Populating Next Right Pointers in Each Node".

What if the given tree could be any binary tree? Would your previous solution still work?

Note:

You may only use constant extra space.

For example,
Given the following binary tree,

         1
       /  \
      2    3
     / \    \
    4   5    7

After calling your function, the tree should look like:

         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \    \
    4-> 5 -> 7 -> NULL

#### 方法：
前边那个没有限定空间复杂度的时候，我们直接可以采用层次遍历的方法，将每一层连接起来。其实之前采用层次遍历方法的时候，我们采用了vector存储每一层节点，遍历到每一层最后节点时，便将vector储存的节点拿出来，依次连接起来。

其实，这个方法还可以简练，观察这棵树的结构，我们可以发现，每当上一层已经连接起来了，我们利用上一层连接信息，便可以把下一层连接起来。

#### C++代码：
```C
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
        TreeLinkNode* mroot = root;
        while(mroot)
        {
            TreeLinkNode* dummy = new TreeLinkNode(0);
            TreeLinkNode* pre = dummy;
            for(auto p = mroot; p; p = p->next)
            {
                if(p->left)
                {
                    pre->next = p->left;
                    pre = pre->next;
                }
                if(p->right)
                {
                    pre->next = p->right;
                    pre = pre->next;
                }
            }
            mroot = dummy->next;
        }
    }
};
```
#### Java代码:
```java
/**
 * Definition for binary tree with next pointer.
 * public class TreeLinkNode {
 *     int val;
 *     TreeLinkNode left, right, next;
 *     TreeLinkNode(int x) { val = x; }
 * }
 */
public class Solution {
    public void connect(TreeLinkNode root) {
        while(root != null){
            TreeLinkNode dummy = new TreeLinkNode(0);
            TreeLinkNode pre = dummy;
            
            for(TreeLinkNode p = root; p != null; p = p.next){
                if(p.left != null){
                    pre.next = p.left;
                    pre = pre.next;
                }
                if(p.right != null){
                    pre.next = p.right;
                    pre = pre.next;
                }
            }
            root = dummy.next;
        }
    }
}
```