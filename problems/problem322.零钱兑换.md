# 322. 零钱兑换
给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。
````
输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1
````
## 动态规划法
这是一道比较基本的动态规划问题。

凑成面值为11的最小硬币数可以由以下3者的最小值得到：
1. 凑成面值为10的最小硬币数+面值为1的这一枚硬币
2. 凑成面值为9的最小硬币数+面值为2的这一枚硬币
3. 凑成面值为6的最小硬币数+面值为5的这一枚硬币
即dp[11] = min(dp[10]+1, dp[9]+1, dp[6]+1)

定义状态 dp[i]：凑齐总价值i需要的最少硬币数，状态就是问的问题。  
状态转移方程：
````
 dp[amount] = min(1 + dp[amount - coin[i]]) for i in [0, len - 1] if coin[i] <= amount
 ````
 
 需要注意以下两点：
 1. 硬币的面值首先要小于等于当前要凑出来的面值
 2. 剩余的那个面值要能够凑出来，否则这个面值对应的状态应该设置为一个不可能的值
 
 ````cpp
 class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1, amount + 1);
        dp[0] = 0;

        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (i - coin >= 0 && dp[i - coin] != amount + 1)
                    dp[i] = min(dp[i], dp[i - coin] + 1);
            }
        }
        if (dp[amount] == amount + 1)
            dp[amount] = -1;
        return dp[amount];
    }
};
 ````

## dfs法
来自https://leetcode-cn.com/problems/coin-change/solution/322-by-ikaruga/
````cpp
class Solution {
public:
    void coinChange(vector<int>& coins, int amount, int c_index, int count, int& ans) {
        if (amount == 0) {
            ans = min(count, ans);
            return;
        }

        if (c_index == coins.size())
            return;
        
        //k是这次丢的硬币数量，count是之前已经丢的硬币数量，加起来就是一共丢的硬币数量
        //如果比已经找到的ans解还要大，就算往后凑好了钱，也比ans多，没有意义。
        for (int k = amount / coins[c_index]; k >= 0 && k + count < ans; k--)
            coinChange(coins, amount - k * coins[c_index], c_index + 1, count + k, ans);
    }

    int coinChange(vector<int>& coins, int amount) {
        if (amount == 0)
            return 0;
        sort(coins.rbegin(), coins.rend()); //将coins从大到小排序
        int ans = INT_MAX;
        coinChange(coins, amount, 0, 0, ans);
        return ans == INT_MAX ? -1 : ans;
    }
};
````
