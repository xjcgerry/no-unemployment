# 409. 最长回文串
````cpp
class Solution{
public:
  int longestPalindrome(string s)
  vector<int> m(128,0);
  int len = 0;
  while (auto c:s) {
    if (m[c]&1) len+=2; //m[c]&1判断m[c]是否为奇数，如果是奇数，则结果为1，否则结果是0
    m[c]++;
  }
  if (len<s.size()) len++;
  return len;
};
````
对于“abccccdd”来说，m[a] = 1, m[b] = 1, m[c] = 4, m[d] = 2.  
在第一次遇到a的时候，m[a]是0，len不增加，记录a出现的次数为1
