# 102. 二叉树的层次遍历
迭代，广度优先遍历比较利于理解
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> res;

        if (root == NULL) return {};
        queue<TreeNode*> q;
        q.push(root);

        while (!q.empty()) {
            vector<int> level;  //存放每一层的元素值
            int count = q.size();   //表示当前层的元素个数
            while (count--) {
                TreeNode* t = q.front();
                q.pop();
                level.push_back(t->val);
                if (t->left) q.push(t->left);
                if (t->right) q.push(t->right);
            }
            res.push_back(level);
        }
        return res;
    }
};