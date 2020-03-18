# 100. 相同的树
递归
````cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p == NULL && q == NULL) return true;
        if (p == NULL || q== NULL) return false;
        if (p->val != q->val) return false;
        return isSameTree(p->right, q->right) && isSameTree(p->left, q->left);
    }
};
````
