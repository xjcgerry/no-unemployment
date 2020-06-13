# 10. 正则表达式匹配
我要记住这个日子，2020/3/25，这道题我做了半天  
参考答案：https://leetcode-cn.com/problems/regular-expression-matching/solution/dong-tai-gui-hua-zen-yao-cong-0kai-shi-si-kao-da-b/  
````cpp
class Solution {
public:
    bool isMatch(string s, string p) {
    int slen = s.size();
    int plen = p.size();
    if (plen == 0) {
        return slen == 0; 
    }
    if (slen == 0 && plen == 1) {
        return false; 
    }

    //1. 初始条件
    bool dp[slen+1][plen+1];
    dp[0][0] = true;
    dp[0][1] = false; 
    for(int i = 2; i < plen+1; i++) { //初始化第0行
        dp[0][i] = (p[i-1] == '*' && dp[0][i-2]); //s是空的，p是非空的。P=“.*”或者“#*”能够匹配，其他的都不能匹配
    }
    for(int i = 1; i < slen+1; i++) { //初始化第0列
        dp[i][0] = false;
    }

    //2. 填表
    for(int i = 1; i < slen+1; i++) {
        for(int j = 1; j < plen+1; j++) {            
            if (j >= 2 && p[j-1] == '*') {  //p的下标从0开始，第j-1个为*
                bool t1 = dp[i-1][j] && (p[j-2] == s[i-1] || p[j-2] == '.');  //多个字符匹配；后半部分：匹配一次or万能
                bool t2 = dp[i][j-2]; //没有字符匹配，相当于去掉c*
                dp[i][j] = t1 || t2;
            } else if (p[j-1] == '.' || p[j-1] == s[i-1]) {
                dp[i][j] = dp[i-1][j-1];
            } else {                
                dp[i][j] = false; 
            }
        }
    }

    return dp[slen][plen]; 
    }
};
````
