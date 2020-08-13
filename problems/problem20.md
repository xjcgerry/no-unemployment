# 20. 有效的括号

利用栈进行括号配对
````cpp
class Solution {
public:
    bool isValid(string s) {
        unordered_map<char, int> m{{'(',1},{'[',2},{'{',3},{')',4},{']',5},{'}',6}};
        stack <char> st;
        bool istrue = true;
        for (char c:s){
            int flag = m[c];
            if (flag >= 1 && flag <= 3) st.push(c);
            else if (!st.empty()&&m[st.top()] == flag-3) st.pop();
            else 
            {
                istrue = false;
                break;
            }
        }
        if (!st.empty()) istrue = false;    //如果前面的都匹配完了，栈里还有括号，说明invalid
        return istrue;
    }
};
````

不用map容器，只利用栈
````cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        //意思就是，下一个字符要么是左括号，要么是与之匹配的右括号，否则就不行
        for (int i = 0; i < s.size(); i++) {
            if (s[i] == '(') st.push(')');
            else if (s[i] == '{') st.push('}');
            else if (s[i] == '[') st.push(']');
            // 第三种情况 是遍历字符串匹配的过程中，栈已经为空了，没有匹配的字符了，说明右括号没有找到对应的左括号 return false
            // 第二种情况 遍历字符串匹配的过程中，发现栈里没有我们要匹配的字符。所以return false
            else if (st.empty() || st.top() != s[i]) return false;
            else st.pop(); // st.top() == s[i]
        }
        // 第一种情况 此时我们已经遍历完了字符串，但是栈不为空，说明有相应的左括号没有右括号来匹配，所以return false，否则就return true
        return st.empty();
    }
};
````
