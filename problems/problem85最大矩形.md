# 85. 最大矩形
根据84的解，对每一行的数据求当前的最大矩形。
````cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        int res = 0;
        heights.push_back(0);
        stack<int> s;
        s.push(-1);
        for (int i = 0; i < heights.size(); i++) {
            if (i == 0 || s.size() == 1 || heights[i] >= heights[s.top()])
                s.push(i);
            while (s.size() > 1 && heights[i] < heights[s.top()]) {
                int cur = s.top();
                s.pop();
                res = max(res, (i - s.top() - 1)*heights[cur]);
            }
            s.push(i);
        }
        return res;
    }
    int maximalRectangle(vector<vector<char>>& matrix) {
        if (matrix.size() == 0) return 0;
        int m = matrix.size();
        int n = matrix[0].size();
        vector<int> v(n, 0);
        int ans = 0;
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++){
                v[j] = matrix[i][j]=='1' ? v[j] + 1 : 0;
            }
            ans = max(ans, largestRectangleArea(v));
        }
        return ans;
    }
};
````
