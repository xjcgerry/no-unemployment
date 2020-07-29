````cpp
class Solution {
private:
    vector<int> candidates;
    vector<vector<int>> res;
    vector<int> cur;

public:
    void DFS(int start, int target) {
        if (target == 0) {
            res.push_back(cur);
            return;
        }
        for (int i = start; i < candidates.size() && target - candidates[i] >= 0; i++) {
            cur.push_back(candidates[i]);
            DFS(i, target - candidates[i]);
            cur.pop_back();
        }
    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        this->candidates = candidates;
        DFS(0, target);
        return res;
    }
};
````
