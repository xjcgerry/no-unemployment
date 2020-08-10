给定一个字符串 s，计算具有相同数量0和1的非空(连续)子字符串的数量，并且这些子字符串中的所有0和所有1都是组合在一起的。

重复出现的子串要计算它们出现的次数。

示例1：
````
输入: "00110011"
输出: 6
解释: 有6个子串具有相同数量的连续1和0：“0011”，“01”，“1100”，“10”，“0011” 和 “01”。

请注意，一些重复出现的子串要计算它们出现的次数。

另外，“00110011”不是有效的子串，因为所有的0（和1）没有组合在一起。
````
示例2：
````
输入: "10101"
输出: 4
解释: 有4个子串：“10”，“01”，“10”，“01”，它们具有相同数量的连续1和0。
````

# 1、分组
将字符串看做由很多组连续的0和1构成，统计每组0或1的个数，那么相邻两组能满足题意的子串数量为min(count[i - 1], count[1])
````cpp
int countBinarySubstrings(string s)
{
    int n = s.size();
    vector<int> num;
    int count = 1;
    for (int i = 0; i < n - 1; i++)
    {
        if (s[i] == s[i + 1])
        {
            count++;
        }
        else
        {
            num.push_back(count);
            count = 1;
        }
    }
    num.push_back(count);
    int res = 0;
    for (int i = 1; i < num.size(); i++)
    {
        res += min(num[i], num[i - 1]);
    }
    return res;
}
````

# 2、中心扩展法
从一对不同的0和1开始，两边扩展，与同边的数字相等就+1，否则就往后寻找下一对0和1。
````cpp
class Solution {
public:
    int countBinarySubstrings(string s) {
        int n = s.size();
        int count = 0;
        for (int i = 1; i < n; i++) {
            int left = i - 1;
            int right = i;
            char cleft = s[left];
            char cright = s[right];
            if (cleft == cright)
                continue;
            while (left >= 0 && right < n && s[left] == cleft && s[right] == cright) {
                left--;
                right++;
                count++;
            }
        }
        return count;
    }
};
````
