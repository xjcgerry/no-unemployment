给定一个字符串 s，你可以通过在字符串前面添加字符将其转换为回文串。找到并返回可以用这种方式转换的最短回文串。

示例1：
````
输入: "aacecaaa"
输出: "aaacecaaa"
````
示例2：
````
输入: "abcd"
输出: "dcbabcd"
````

# 暴力法
寻找字符串s中的最大回文子串，找到了就直接返回。因为是在前面添加字符，所以以0为子串开头，子串结尾从n开始往前进
````cpp
string shortestPalindrome(string s)
{
    int n = s.size();
    string rev(s);
    reverse(rev.begin(), rev.end());
    for (int i = 0; i < n; i++) {
        if (s.substr(0, n - i) == rev.substr(i))
            return rev.substr(0, i) + s;
    }
    return "";
}
````

# 网易笔试题
是在字符串后面添加字符，反过来思考即可。

也是寻找最大子串，因为是在后面添加，所以每次子串的结尾都是n，子串的开头从0开始往后递增
````cpp
#include <string>
#include <algorithm>

using namespace std;

string shortestPalindrome(string s)
{
    int n = s.size();
    string rev(s);
    reverse(rev.begin(), rev.end());
    for (int i = 0; i < n; i++)
    {
        string s1 = s.substr(i);
        string s2 = rev.substr(0, n - i);
        if (s1 == s2)
            return s + s.substr(0, i);
    }
    return "";
}

int main() {
    string ss = "moo";
    string res = shortestPalindrome(ss);
    return 0;
}
````
