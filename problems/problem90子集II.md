````cpp
class Solution {
public:
    vector<int> cur;
    vector<vector<int>> res;
    void dfs(vector<int>& nums, int start) {
        //这里为啥没有跳出递归的条件？
        res.push_back(cur);
        for (int i = start; i < nums.size(); i++) {
            if (i > start && nums[i] == nums[i - 1])
                continue;
            cur.push_back(nums[i]);
            dfs(nums, i + 1);
            cur.pop_back();
        }
    }

    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        //有重复数字的，需要先排序
        sort(nums.begin(), nums.end());

        dfs(nums, 0);
        return res;
    }
};
````
