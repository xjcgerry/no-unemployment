# 40. 通配符匹配
## 贪心算法
双指针，iStar和jStar表示*在s和p中匹配的位置。i和j表示当前匹配的位置。
````cpp
class Solution {
public:
    bool isMatch(string s, string p) {
        int i = 0, j = 0, iStar = -1, jStar = -1, m = s.size(), n = p.size();
        while (i < m) {
            if (j < n && (s[i] == p[j] || p[j] == '?')) {
                ++i;
                ++j;
            }
            else if (j < n && p[j] == '*') {
                iStar = i;  //  记录星号位置
                jStar = j++;    //记录星号位置，并把j移到下一位，准备下一个循环匹配
            }
            else if (iStar >= 0) {   //字符不匹配，且没有星号出现，但是IStar>0，说明*匹配的字符数量不对，回溯
                i = ++iStar;
                j = jStar + 1;
            }
            else
                return false;
        }
        while (j < n && p[j] == '*')   ++j;    //去除多余星号
        return j == n;
    }
};
````
