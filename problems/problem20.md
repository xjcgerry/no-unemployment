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
            else {istrue = false; break;}
        }
        if (!st.empty()) istrue = false;    //如果前面的都匹配完了，栈里还有括号，说明invalid
        return istrue;
    }
};
````
