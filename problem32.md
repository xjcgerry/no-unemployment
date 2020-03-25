# 32. 最长有效括号
## 暴力法
判断括号匹配问题一般用栈解决
````cpp
class Solution {
public:
    bool isValid (string s) { //先定义函数isValid判断一个字符串是不是配对
        stack<char> a;
        for (auto v : s) {
            if (v == '(')
                a.push(v);
            else if (!a.empty() && a.top() == '(')    //不是(,肯定是),所以配对成功，pop
                a.pop();
            else
                return false;
        }
        return a.empty();
    }

    int longestValidParentheses(string s) {
        int maxLen = 0;
        for (int i = 0; i < s.size(); i++) {
            for (int j = 2; j + i <= s.size(); j += 2) {
                if (isValid(s.substr(i,j))) //substr 从i开始，长度为j的子串
                    maxLen = max(maxLen, j);
            }
        }
        return maxLen;
    }
};
````
## 动态规划
定义dp[i]为到第i个格子位置，匹配的子串长度  
如果s[i] = '('，那么肯定不匹配，说明dp[i] = 0  
如果s[i] = ')'
* 如果s[i-1] = '('，刚好配对，本身长度为2，所以dp[i] = dp[i - 2]
* 如果s[i-1] = ')'，要进一步考虑这个子串之前时候有'('，如果能匹配成新的子串。  
那么s[i-1] == ')' && s[i-dp[i-1]-1] == '('，能匹配成功。长度为dp[i-dp[i-1]-2] + dp[i-1] + 2    

因为有i-2，为了防止越界，在s开头插入两个')'，在dp比较方便
````cpp
class Solution {
public:
    int longestValidParentheses(string s) {
        pair<char, char> k = {'(', ')'};
        s.insert(s.begin(), k.second);
        s.insert(s.begin(), k.second);
        vector<int> dp(s.size(), 0);
        int ans = 0;
        for (int i = 2; i< s.size(); i++) {
            if (s[i] == k.first)
                dp[i] = 0;
            else {
                if (s[i-1] == k.first)
                    dp[i] = dp[i-2] + 2;
                else if (s[i - dp[i-1] - 1] == k.first)
                    dp[i] = dp[i- dp[i-1] - 2] + 2 + dp[i-1];
            }
            ans = max(ans,dp[i]);
        }
        return ans;
    }
};
````
