# 72. 编辑距离
给你两个单词 word1 和 word2，请你计算出将 word1 转换成 word2 所使用的最少操作数 。

你可以对一个单词进行如下三种操作：

插入一个字符  
删除一个字符  
替换一个字符  

## 思路

来自：https://leetcode-cn.com/problems/edit-distance/solution/edit-distance-by-ikaruga/

动态规划

* 定义dp[i][j]，代表word1前i个字符，变换到word2前j个字符，最短需要操作的次数  
* 考虑word1和word2一个字母都没有，即全增加/删除的情况，预留dp[0][j]和dp[i][0]

状态转移  
1. 增，dp[i][j] = dp[i][j - 1] + 1，word2增加一个字符可以得到word1
2. 删，dp[i][j] = dp[i - 1][j] + 1，word1删除第i个字符可以得到word2
3. 改，dp[i][j] = dp[i - 1][j - 1] + 1，word1或者word2修改一个字符可以得到对方
4. 按顺序计算，当计算dp[i][j]时，dp[i][j - 1]，dp[i - 1][j]，dp[i - 1][j - 1]都已经确定了
5. 配合增、删、改这三种操作，需要对应的dp把操作次数加一，取三种的最小
6. 如果刚好word1[i-1]和word2[j-1]两个字母相同，可以参考dp[i-1][j-1]，操作不用加一

````cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        vector<vector<int>> dp(word1.size() + 1, vector<int>(word2.size() + 1, 0));

        for (int i = 0; i < dp.size(); i++)
            dp[i][0] = i;
        for (int j = 0; j < dp[0].size(); j++)
            dp[0][j] = j;

        for (int i = 1; i < dp.size(); i++) {
            for (int j = 1; j < dp[0].size(); j++) {
                dp[i][j] = min(dp[i - 1][j - 1], min(dp[i - 1][j], dp[i][j - 1])) + 1;
                if (word1[i - 1] == word2[j - 1])
                    dp[i][j] = min(dp[i][j], dp[i - 1][j - 1]);
            }
        }
        return dp.back().back();
    }
};
````
