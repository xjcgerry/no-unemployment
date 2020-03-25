# 95. 不同的二叉搜索树 II
二叉搜索树其实就是二叉排序树，左子树上所有结点的值小于其根结点的值，右子树上所有结点的值大于其根结点的值。
## 递归实现
1作为根节点，则左子树为空，右子树为【2……n】  
2作为根节点，则左子树为【1】，右子树为【3……n】  
3作为根节点，则左子树为【1 2】，右子树为【4……n】，左右子树两两组合  
.  
.  
.  
n作为根节点，则左子树为【1……n-1】，右子树为空

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
    vector<TreeNode*> getTree(int begin, int end) {
        vector<TreeNode*> res;
        if (begin > end) {
            res.push_back(NULL);
            return res;
        }

        for (int i = begin; i <= end; i++) {
            vector<TreeNode*> leftNode = getTree(begin, i-1);
            vector<TreeNode*> rightNode = getTree(i+1, end);
            for (auto left:leftNode) {
                for (auto right:rightNode){
                    TreeNode* root = new TreeNode(i);
                    root->left = left;
                    root->right = right;
                    res.push_back(root);
                }
            }
        }
        return res;
    }
    vector<TreeNode*> generateTrees(int n) {
        if (n == 0)
            return vector<TreeNode*>();
        return getTree(1,n);
    }
};
````

## 动态规划
这tm是什么恶心的方法，每次一看就厌学
