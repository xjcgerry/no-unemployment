````cpp
class Solution {
public:
    vector<int> cur;
    vector<vector<int>> res;

    void dfs(vector<int>& candidates, int start, int target) {
        if (target == 0) {
            res.push_back(cur);
            return;
        }
        for (int i = start; i < candidates.size() && target - candidates[i] >= 0; i++) {
            //因为可以重复使用一个数字，所以依然从start开始，看这个数字能不能用
            //start之前的数因为之前的分支搜索过了，所以会产生重复
            //target - candidates[i] >= 0的条件相当于是剪枝
            cur.push_back(candidates[i]);
            dfs(candidates, i, target - candidates[i]);
            cur.pop_back();
        }
    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end()); //对数组排序，后续可以剪枝
        dfs(candidates, 0, target);
        return res;
    }
};
````
