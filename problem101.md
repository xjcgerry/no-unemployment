# 101. 对称二叉树
## 递归
````cpp
*Definition for a binary tree node.
*struct TreeNode{
*     int val;
*     TreeNode* left;
*     TreeNode* right;
*     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
* };

class solution {
public:
    bool isSymmetric(TreeNode* root) {
        if (root == NULL) return true;
        return isMirror(root->left, root->right);
    }
    bool isMirror(TreeNode* p, TreeNode* q) {
        if (p == NULL && q == NULL) return true;
        if (p == NULL || q == NULL) return false;
        if (p->val != q->val) return false;
        return isMirror(p->left, q->right) && isMirror(p->right, q->left);
    }
}
````
## 迭代
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
    bool isSymmetric(TreeNode* root) {
        if (root == NULL) return true;
        queue<TreeNode*> quk;
        quk.push(root->left);
        quk.push(root->right);
        while (!quk.empty()) {
            TreeNode* t1 = quk.front();
            quk.pop();
            TreeNode* t2 = quk.front();
            quk.pop();
            if (t1 == NULL && t2 == NULL) continue;
            if (t1 == NULL || t2 == NULL) return false;
            if (t1->val != t2->val) return false;
            quk.push(t1->left);
            quk.push(t2->right);
            quk.push(t1->right);
            quk.push(t2->left);
        }
        return true;
    }
};
````
