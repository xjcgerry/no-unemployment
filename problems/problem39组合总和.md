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
        for (int i = start; i < candidates.size() && target >= candidates[i]; i++) {
            cur.push_back(candidates[i]);
            dfs(candidates, i, target - candidates[i]);
            cur.pop_back();
        }
    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        dfs(candidates, 0, target);
        return res;
    }
};
````
