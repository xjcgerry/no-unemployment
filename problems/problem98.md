# 98. 验证二叉树
## 递归
引入上下边界，对于每个节点，设其上下边界为low和high，判断根节点时，必须满足low < root->val < high  
对于左节点，上边界变为根结点的值root->val  
对于右节点，下边界变为根结点的值root->val  
因为样例中有INT_MAX的数据，因此边界定义为long型的变量
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
    bool fun(TreeNode* root, long low, long high) {
        if (root == NULL) return true;
        long num = root->val;
        if (num <= low ||num >= high) return false;
        return fun(root->left, low, num) && fun(root->right, num, high);
    }

    bool isValidBST(TreeNode* root) {
        return fun(root, LONG_MIN, LONG_MAX);
    }
};
````
## 中序遍历
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
    bool isValidBST(TreeNode* root) {
        bool flag = true;
        vector<int> v;
        stack<TreeNode*> s;

        if (!root)
            return true;
        
        while (root || !s.empty()) {
            while (root) {
                s.push(root);
                root = root->left;
            }
            if (!s.empty()) {
                root = s.top();
                s.pop();
                v.push_back(root->val);
                root = root->right;
            }
        }
        for (int i = 0; i < v.size()-1; i++) {  //这里要注意i<v.size()-1，否则i+1会超过容器中实际的数值。
            if (v[i] >= v[i+1]) 
                flag = false;
        }
        
        return flag;
    }
};
````
