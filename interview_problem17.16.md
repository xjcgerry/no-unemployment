# 面试题17.16. 按摩师
首次接触动态规划问题
设到第n个预约的最大时长为dp[n]，如果我们接第n个预约的话，由于相邻的预约不能接，所以dp[n] = dp[n-2] + nums[n]; 如果我们不接第n个预约的话，那么 dp[n] = dp[n-1]  
状态转移方程为 dp[i] = max(dp[i-1], dp[i-2] + nums[i])
````cpp
class Solution {
public:
    int massage(vector<int>& nums) {
        int n = nums.size();
        if (n == 0)
            return 0;
        if (n == 1)
            return nums[0];

        vector<int> dp(n);
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);
        for (int i = 2; i < n; i++)
            dp[i] = max(dp[i-1], dp[i-2] + nums[i]);

        return dp[n-1];
    }
};
````
## 优化空间复杂度
i只依赖于i-1和i-2两个状态，只要定义两个变量来存储i-1和i-2两个状态就行了。  
用a表示i-2，b表示i-1，则dp[i] = max(a, b+nums[i])  
在下一轮循环的时候，i-1变成了i-2，把b的值赋给a；i变成了i-1，把dp[i]的值赋给b  
````cpp
class Solution {
public:
    int massage(vector<int>& nums) {
        int a = 0, b = 0;
        for (int i = 0; i < nums.size(); i++) {
            int c = max(b, a + nums[i]);
            a = b;
            b = c;
        }
        return b;
    }
};
````
