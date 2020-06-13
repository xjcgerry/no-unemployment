# 287. 寻找重复数
## 二分查找
n+1的数组中有1~n中的数，至少有一个重复的。虽然nums数组是无序的，但是只需要统计nums在[left,mid]之间的数，如果大于mid，说明重复的数在mid左边，否则在mid右边。
````cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int len = nums.size();
        int left = 1;
        int right = len-1;
        while (left < right) {
            int mid = (left + right) / 2;
            int cnt = 0;
            for (int num : nums) {
                if (num <= mid)
                    cnt += 1;
            }
            if (cnt > mid) {
                right = mid;
            }
            else {
                left = mid + 1;
            }
        }
        return left;
    }
};
````
