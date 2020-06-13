# 96. 不同的二叉搜索树
## 动态规划
定义dp(n+1)用于保存1……n个节点组成的二叉搜索树的个数。  
首先看边界条件  
* dp[0] = 1，没有树也算作一种
* dp[1] = 1，只有一个根结点

如果以i为根结点，那么[1..i-1]为左子树，共有dp[i-1]种；[i+1..n]为右子树，共有dp[n-i]种。所以该种情况下共有dp[i-1] * dp[n-i]种结构。
所以1……n个节点的情况下，就是把从1到n，把这些结果相加。  
````cpp
class Solution {
public:
    int numTrees(int n) {
        if (n == 0) return 1;

        vector<int> dp(n+1);
        dp[0] = 1;
        dp[1] = 1;

        for (int end  = 2; end <= n; end++) {
            for (int mid = 1; mid <= end; mid++){
                dp[end] += dp[mid-1] * dp[end - mid];
            }
        }
        return dp[n];

    }
};
````
