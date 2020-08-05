你是一个专业的小偷，计划偷窃沿街的房屋，每间房内都藏有一定的现金。这个地方所有的房屋都围成一圈，这意味着第一个房屋和最后一个房屋是紧挨着的。同时，相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你在不触动警报装置的情况下，能够偷窃到的最高金额。

示例1：
````cpp
输入: [2,3,2]
输出: 3
解释: 你不能先偷窃 1 号房屋（金额 = 2），然后偷窃 3 号房屋（金额 = 2）, 因为他们是相邻的。
````

示例2：
````cpp
输入: [1,2,3,1]
输出: 4
解释: 你可以先偷窃 1 号房屋（金额 = 1），然后偷窃 3 号房屋（金额 = 3）。
     偷窃到的最高金额 = 1 + 3 = 4 。
````

````cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() == 1)
            return nums[0];
        int n = nums.size();
        vector<int> dp1(n + 1);
        vector<int> dp2(n + 1);
        for (int i = 2; i <= n; i++) {
            dp1[i] = max(dp1[i - 1], dp1[i - 2] + nums[i - 2]);     //不算最后一间房屋
            dp2[i] = max(dp2[i - 1], dp2[i - 2] + nums[i - 1]);     //不算第一间房屋
        }
        return max(dp1[n], dp2[n]);
    }
};
````

````cpp
class Solution {
public:
    int myRob(vector<int>&nums) {
        int pre = 0, cur = 0, tmp;
        for (int num : nums) {
            tmp = cur;
            cur = max(pre + num, cur);
            pre = tmp;
        }
        return cur;
    }

    int rob(vector<int>& nums) {
        if (nums.size() == 0) return 0;
        if (nums.size() == 1) return nums[0];

        vector<int>::iterator it = nums.begin();
        int n = nums.size();
        vector<int> nums1 = vector<int>(it, it + n - 1);
        vector<int> nums2 = vector<int>(it + 1, it + n);
        return max(myRob(nums1), myRob(nums2));
    }
};
````
