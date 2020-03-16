# 71. 简化路径
````cpp
class Solution {
public:
    string simplifyPath(string path) {
        stringstream is(path);
        vector<string> strs;
        string res = "", tmp = "";
        while (getline(is, tmp, '/')) {//指定getline的结束符为“/”
            if(tmp == "" || tmp == ".")//如果是当前目录，就不进行操作
                continue;
            else if (tmp == ".." && !strs.empty())//如果要返回上一级，且栈内非空，就弹出栈顶元素
                strs.pop_back();
            else if (tmp != "..")//如果都不是，就进栈。一般是遇到字母了
                strs.push_back(tmp);
        }
        for (string str:strs)
            res += "/" +str;
        if (res.empty())
            return "/";
        return res;

    }
};
````
