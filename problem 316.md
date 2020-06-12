# 316. 去除重复字母
## 思路
例如，“bcabc”。读到bc，这是当前最小的字典序了。继续往后读的话，a比c小，并且后面还有c，所以舍弃c，留下a。对于b也同理，因此需要借助栈。  
流程：
1. 遍历字符串里的字符，如果读到的字符是升序的，就存到栈里
2. 如果读到的字符在栈中已经存在，则这个字符不需要
3. 如果读到的字符比栈顶的元素小，此时看一下栈顶元素在字符串后面是否还会出现，如果还会出现一次，就舍弃栈顶元素，选择后出现的字符。

由于需要查找字符，而栈没有对应的查找函数，因此用一个string类型的stk变量来表示栈。  
这里要注意的是，对于string.find函数，如果没有查找到，则string.find(c) == string::npos来表示。

````cpp
class Solution
{
public:
    string removeDuplicateLetters(string s)
    {
        string stk;
        for (int i = 0; i < s.size(); i++) {
            char c = s[i];
            if (stk.find(c) != string::npos)
                continue;
            while (!stk.empty() && stk.back() > c && s.find(stk.back(), i) != string::npos)
                stk.pop_back();
            stk.push_back(c);
        }
        return stk;
    }
};
````
