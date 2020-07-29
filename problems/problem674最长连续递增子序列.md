````cpp
class Solution {
public:
    int findLengthOfLCIS(vector<int>& nums) {
        if (nums.size() == 0)
            return 0;
        int ans = 1;
        int cur = 1;
        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] > nums[i - 1]) {
                cur++;
                ans = max(cur, ans);
            }
            else {
                cur = 1;
            }
        }
        return ans;
    }
};
````
