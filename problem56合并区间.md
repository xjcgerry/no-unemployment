# 56. 合并区间
````cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        if (intervals.size() == 0 || intervals.size() == 1) return intervals;
        int u = 0, v = 0;
        vector<vector<int>> ans;
        std::sort(intervals.begin(), intervals.end());
        while (v < intervals.size()) {
            if (intervals[u][1] < intervals[v][0]) {
                ans.emplace_back(intervals[u]);   //用emplace_back效率更高。因为push_back要调用构造函数
                u = v;
                v++;
            } else if (intervals[u][1] >= intervals[v][1]) {
                v++;
            } else {
                intervals[u][1] = intervals[v][1];
                v++;
            }
        }
        ans.emplace_back(intervals[u]);
        return ans;
    }
};
````
