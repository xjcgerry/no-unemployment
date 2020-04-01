# 15. 三数之和
## 双指针法
既然要用双指针，所以首先要排序sort()，时间复杂度为nlogn。然后指定第一个数nums[i]，第二个数为nums[L]，第三个数为nums[R]。  
如果nums[i] == nums[i-1]，说明这一轮与上一轮重复了，这一轮跳过。  
L从i+1开始递增，R从size-1开始递减。  
如果三数之和等于0，就记录这一轮的三个数，然后继续递增L，递减R；否则三数之和小于0，就递增L；大于0，就递减R。  
````cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> ans;
        int size = nums.size();
        if (size < 3) 
            return ans;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < size; i++) {
            if (nums[i] > 0)    //如果当前数字大于0，那么三数之和肯定大于0，跳出循环
                break;
            if (i > 0 && nums[i] == nums[i-1])   //去重
                continue;
            int L = i + 1;
            int R = size - 1;
            while (L < R) {
                int sum = nums[i] + nums[L] + nums[R];
                if (sum == 0) {
                    ans.push_back(vector<int>{nums[i], nums[L], nums[R]});
                    while (L < R && nums[L] == nums[L+1]) L++;
                    while (L < R && nums[R] == nums[R-1]) R--;
                    L++;
                    R--;
                }
                else if (sum < 0) L++;
                else if (sum > 0) R--;
            }
        }
        return ans;
    }
};
````
