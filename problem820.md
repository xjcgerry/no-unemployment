# 820. 单词的压缩编码
只有一个单词完全包含另一个单词，才能让两个单词放进一个编码。
不借助字典树，利用反转+排序的方法。
如果有一对单词s和t，使得t是s的后缀，例如me是time的后缀，就删掉单词t。最后剩下来的就是构成索引字符串的单词。  
把所有单词反转，让倒的变成正的。所有单词反转之后，我们的单词排序规则就变成了字典顺序。这样，如果t是s的后缀，那么反转之后t'是s'的前缀。而且反转+排序之后，
s'一定紧跟在t'的后面。
````cpp
class Solution {
public:
    int minimumLengthEncoding(vector<string>& words) {
        int N = words.size();
        vector<string> reversed_words;
        for (string word : words) {
            reverse(word.begin(), word.end());
            reversed_words.push_back(word);
        }
        sort(reversed_words.begin(),reversed_words.end());

        int res = 0;
        for (int i = 0; i < N; i++) {
            if (i + 1 < N && reversed_words[i+1].find(reversed_words[i]) == 0) {  //  如果前一个单词是后一个单词前缀
                                                                                  //  什么都不操作，相当于丢弃
            } else {
                res += reversed_words[i].size() + 1;  //否则，就加上这个单词的长度，并加上#
            }
        }
        return res;
    }
};
````
