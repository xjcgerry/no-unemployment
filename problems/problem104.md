# 104. 二叉树的最大深度
## 深度优先搜索DFS 递归
每个节点只访问一次，时间复杂度为O(n)
在最糟糕的情况下，树完全不平衡，递归将会被调用N次，因此保持调用栈的存储将是O(n)。在最好情况下，树是完全平衡的，树的高度是log(n)，这种情况下空间复杂度是O(logn)
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
    int maxDepth(TreeNode* root) {
        if (root == NULL) return 0;
        int l = maxDepth(root->left) + 1;
        int r = maxDepth(root->right) + 1;
        return l > r ? l : r;
    }
};
````
## 深度优先搜索 迭代
先走到二叉树的最左边，记录下最左边节点的信息和深度。
````cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == NULL)
            return 0;
        stack<pair<TreeNode*, int>> s;
        TreeNode* p = root;
        int maxDepth = 0;
        int depth = 0;
        while(!s.empty() || p != NULL) {  //栈非空，说明还有右子树未探索；若p非空，说明还有左子树未探索
            while (p != NULL) { //先往左边走
                s.push(pair<TreeNode*, int>(p, ++depth));
                p = p->left;
            }
            p = s.top().first;
            depth = s.top().second;
            if(maxDepth < depth)
                maxDepth = depth;
            s.pop();  //将当前左子树出栈，此时栈顶为当前左子树的根结点，在下一轮迭代中，会转向右子树
            p = p->right;
        }
        return maxDepth;
    }
};
````
## 广度优先搜索BFS
时间复杂度 O(n)
空间复杂度 O(n)
````cpp
class Solution {
public:
    int maxDepth(TreeNode* root) {
        if (root == NULL) 
            return 0;
        deque<TreeNode*> q;
        q.push_back(root);
        int depth = 0;
        while (!q.empty()) {
            depth++;
            int num = q.size();
            for (int i = 1; i <= num; i++) {
                TreeNode* p = q.front();
                q.pop_front();
                if (p->left) q.push_back(p->left);
                if (p->right) q.push_back(p->right);
            }
        }
        return depth;
    }
};
````
