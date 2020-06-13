# 107. 二叉树的层次遍历 II
有两种做法，一是根据102题得到的结果，reverse一下就行了，还是考的广度优先搜索，这里就不写了

## 递归？？
构造一个helper函数，递归调用，helper函数按照从叶子往根部的顺序，往res容器里插入每一层的节点，这样最后得到的结果就是逆序的了。
````cpp
class Solution {
public:
    vector<vector<int>> res;
    void levelOrderBottomHelper(queue<TreeNode*> curLevel) {
        queue<TreeNode*> nextLevel;
        vector<int> vals;
        while(!curLevel.empty()) {
            TreeNode* root = curLevel.front();
            curLevel.pop();
            vals.push_back(root->val);
            if (root->left) nextLevel.push(root->left);
            if (root->right) nextLevel.push(root->right);
        }
        if (!nextLevel.empty())
            levelOrderBottomHelper(nextLevel);
        res.push_back(vals);
    }

    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        queue<TreeNode*> nextLevel;
        if (root != NULL) {
            nextLevel.push(root);
            levelOrderBottomHelper(nextLevel);
        }
        return res;
    }
};
````

## 迭代法
````cpp
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> v;
        if (root == NULL)
            return v;
        queue<TreeNode*> q;
        vector<int> tmp;
        q.push(root);
        while (!q.empty()) {
            int size = q.size();
            for (int i = 0; i < size; i++) {
                if (q.front()->left != NULL)
                    q.push(q.front()->left);
                if (q.front()->right != NULL)
                    q.push(q.front()->right);
                tmp.push_back(q.front()->val);
                q.pop();
            }
            v.insert(v.begin(), tmp); //每一次的结果插入容器的头部，这样最后的结果就是逆序的了
            tmp.resize(0);
        }
        return v;
    }
};
````
