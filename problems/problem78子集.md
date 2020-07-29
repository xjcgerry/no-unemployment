````cpp
class Solution {
public:
    void dfs(vector<int> &nums, int pos, vector<int> &list, vector<vector<int>> &result) {
        if (pos == nums.size()) {
            result.push_back(list);
            return;
        }
        list.push_back(nums[pos]);
        dfs(nums, pos+1, list, result);
        list.pop_back();
        dfs(nums, pos+1, list, result);
    }

    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> result;
        vector<int> list;
        dfs(nums, 0, list, result);
        return result;
    }
};
````
