# 5. 最长回文子串
动态规划是最常用的解法  
看不出来动态规划是什么
````cpp
class Solution {
public:
    string longestPalindrome(string s) {
        const int size = s.size();
        if (size < 2) 
            return s;
        
        bool dp[size][size];
        for (int i = 0; i < size; i++)
            dp[i][i] = true;
        
        int start = 0;
        int maxLen = 1;

        for (int j = 1; j < size; j++) {
            for (int i = 0; i < j; i++) {
                if (s[i] == s[j]) {
                    if (j - i <3)   //子串长度小于等于3，只要首尾字符相等就是回文子串了
                        dp[i][j] = true;
                    else
                        dp[i][j] = dp[i+1][j-1];    //j-1列的dp是先计算出来的，所以dp[i][j]可以直接继承它的结果
                } else {
                    dp[i][j] = false;
                }

                if (dp[i][j]) {
                    int curLen = j - i + 1;
                    if (curLen > maxLen) {
                        maxLen = curLen;
                        start = i;
                    }
                }
            }
        }
        return s.substr(start, maxLen);

    }
};
````
