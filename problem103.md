# 103. 二叉树的锯齿形层次遍历
与102题相似，只是需要判断是奇数行还是偶数行。  
迭代，广度优先遍历
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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> res;

        if (root == NULL) return {};
        queue<TreeNode*> q;
        q.push(root);

        int level = 0;
        while (!q.empty()) {
            vector<int> temp;
            int count = q.size();
            while (count--) {
                TreeNode *t = q.front();
                q.pop();
                if (level%2 == 0) temp.push_back(t->val);
                else temp.insert(temp.begin(), t->val);     //往队列头部插入元素
                if (t->left) q.push(t->left);
                if (t->right) q.push(t->right);
            }
            level++;
            res.push_back(temp);
        }
        return res;
    }
};
````
