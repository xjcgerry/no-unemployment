````cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        if (s.size() <= 1)
            return s.size();
        
        int s_len = s.size();
        int start = 0;
        int pos = 1;
        int max_len = 0;

        while (pos < s_len) {
            for (int i = start; i < pos; i++) {
                if (s[i] == s[pos])
                    start = i + 1;
            }
            pos++;
            max_len = max(max_len, pos - start);
        }
        return max_len;
    }
};
````
