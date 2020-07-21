`做这类题最好先把dp表画出来，填好之后分析状态转移方程`
# [72. 编辑距离](https://leetcode-cn.com/problems/edit-distance/)
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

# [583. 两个字符串的删除操作](https://leetcode-cn.com/problems/delete-operation-for-two-strings/)
给定两个单词 word1 和 word2，找到使得 word1 和 word2 相同所需的最小步数，每步可以删除任意一个字符串中的一个字符。

````
输入: "sea", "eat"
输出: 2
解释: 第一步将"sea"变为"ea"，第二步将"eat"变为"ea"
````
这一题跟编辑距离很像，但是两个单词都可以进行更改，注意只能进行删除操作。

采用的思想是下一题的最长公共子序列，找出两个单词的最长公共子序列之后，用单词长度之和减去两倍公共子序列之和即可得到最少的步数。

````cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int len1 = word1.size();
        int len2 = word2.size();
        vector<vector<int>> dp(len1 + 1, vector<int>(len2 + 1));    //这里dp数组中存储的是最长公共子序列长度
        for (int i = 0; i <= len1; i++) {
            for (int j = 0; j <= len2; j++) {
                if (i == 0 || j == 0)
                    dp[i][j] = 0;
                else if (word1[i - 1] == word2[j - 1])      //当前字符相等，在上一个基础上长度加1
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                else                                        //尾端字符对公共子序列没有贡献，此时最长的公共子序列要么是word1[i-1]与word2[j]，要么是word1[i]与word2[j-1]构成
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);     
            }
        }
        return len1 + len2 - 2 * dp[len1][len2];
    }
};
````

# [1143. 最长公共子序列](https://leetcode-cn.com/problems/longest-common-subsequence/)
给定两个字符串 text1 和 text2，返回这两个字符串的最长公共子序列的长度。

一个字符串的 子序列 是指这样一个新的字符串：它是由原字符串在不改变字符的相对顺序的情况下删除某些字符（也可以不删除任何字符）后组成的新字符串。  
例如，"ace" 是 "abcde" 的子序列，但 "aec" 不是 "abcde" 的子序列。两个字符串的「公共子序列」是这两个字符串所共同拥有的子序列。

若这两个字符串没有公共子序列，则返回 0。
![image](https://github.com/xjcgerry/no-unemployment/blob/master/images/1143-1.jpg)

````cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int len1 = text1.size();
        int len2 = text2.size();
        vector<vector<int>> dp(len1 + 1, vector<int>(len2 + 1));
        for (int i = 0; i <= len1; i++) {
            for (int j = 0; j <= len2; j++) {
                if (i == 0 || j == 0)
                    dp[i][j] = 0;
                else if (text1[i - 1] == text2[j - 1])
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                else
                    dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);               
            }
        }
        return dp[len1][len2];
    }
};
````
