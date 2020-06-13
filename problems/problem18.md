# 18. 四数之和
和15.三数之和的思路一样，只是多加一层循环。
````cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> res;
        int size = nums.size();
        if (size < 4) return res;
        sort(nums.begin(), nums.end());

        for (int i = 0; i < size - 3; i++) {
            if (i > 0 && nums[i] == nums[i-1]) continue;    //去重
            for (int j = i + 1; j < size - 2; j++) {
                if (j > i + 1 && nums[j] == nums[j-1]) continue;    //去重
                int L = j + 1;
                int R = size - 1;
                while (L < R) {
                    int sum = nums[i] + nums[j] + nums[L] + nums[R];  //这个要放在while循环内，因为固定了前两个数，后面两个数还需要变化来寻找新的解
                    if (sum == target){
                        res.push_back(vector<int>{nums[i], nums[j], nums[L], nums[R]});
                        while (L < R && nums[L] == nums[L+1]) L++;
                        while (L < R && nums[R] == nums[R-1]) R--;
                        L++;
                        R--;
                    }
                    else if (sum < target) L++;
                    else if (sum > target) R--;
                }
            }
        }
        return res;
    }
};
````
