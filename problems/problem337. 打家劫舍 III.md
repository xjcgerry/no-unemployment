在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

示例1：
````
输入: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
````

示例2：
````
输入: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

输出: 9
解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.
````

# 思路
动态规划的树形版本。用爷爷、2个儿子、4个孙子来说明问题。

问题的状态：爷爷节点如何获取到最大的偷取的钱数  
1. 首先明确相邻的节点不能偷，爷爷选择了偷，儿子就不能偷了，但是孙子可以偷。
2. 二叉树只有左右两个孩子，一个爷爷最多2个儿子，4个孙子。

单个节点的钱怎么算：  
4个孙子偷的钱+爷爷的钱  VS  两个儿子偷的钱。那个组合钱多，就当做当前节点能偷的最大钱数。

4个孙子偷的钱加上爷爷偷的钱
````cpp
int method1 = root->val + rob(root->left->left) + root(root->left->right) + root(root->right->left) + root(root->right->right);
````
两个儿子偷的钱
````cpp
int method2 = rob(root->left) + rob(root->right);
````
挑选一个钱数多的方案
````cpp
int result = max(method1, method2);
````

用一个大小为2的数组来表示vector<int> res = vector<int>(2)，0表示不偷，1表示偷
````cpp
class Solution {
public:
    // first : not to choose current node
    // second : choose current node
    // 类似后续遍历 === 自底向上
    pair<int, int> helper(TreeNode* root) {
        if (root== NULL) return make_pair(0, 0);
        pair<int, int> left= helper(root->left);
        pair<int, int> right= helper(root->right);
        return make_pair(max(left.first, left.second)+ max(right.first, right.second), left.first+ right.first+ root->val);
    }
    int rob(TreeNode* root) {
        pair<int, int> res= helper(root);
        return max(res.first, res.second);
    }
};
````
