# 30. 串联所有单词的子串
字符串匹配，要用到哈希表.
先把单词words都存到一个哈希表m中。然后从s字符串中取子串与哈希表m中的key值进行比较，并把比较结果存入tmp中国，如果tmp与m完全相等，那么就可以匹配上。
````cpp
class Solution {
public:
    vector<int> findSubstring(string s, vector<string>& words) {
        vector<int> res;
        if (s.size() == 0 || words.size() == 0) return res;
        int len = words[0].size();  //单个单词的长度
        int num = words.size();     //单词的个数
        string sub1, sub2;
        unordered_map<string, int> m;
        unordered_map<string, int> tmp;
        for (string t:words)
            m[t]++;
        
        for (int i = 0; i < s.size()-len*num+1; i++) {
            sub1 = s.substr(i, len*num);    //在s字符串中取子字符串sub1
            for (int j = 0; j < sub1.size()-len+1; j += len) {
                sub2 = sub1.substr(j, len);     //在子字符串中取与单个单词等长的子字符串
                if (m.count(sub2) == 0) break;  //看单词的map中是否出现了sub2字符串
                else tmp[sub2]++;
            }
            if (m == tmp) res.push_back(i);
            tmp.clear();
        }
        return res;
    }
};
````
