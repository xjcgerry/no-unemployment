# 4.寻找两个有序数组的中位数
## 前一百题中最难，看似简单，实际看解答看到流眼泪
通过切一刀能够把有序数组分成左右两个部分，割的左右会有两个元素，分别是左边最大值和右边最小值。  
Ci是第i个数组的割，LMaxi第i个数组割后的左元素，RMini为第i个数组割后的右元素。  
LMax1 <= RMin1, LMax2 <= RMin2这是肯定的  
如果让 LMax1 <= RMin2, LMax2 <= RMin1，那么左半边就全部小于右半边。  
太多了，不想写了https://leetcode-cn.com/problems/median-of-two-sorted-arrays/solution/4-xun-zhao-liang-ge-you-xu-shu-zu-de-zhong-wei-shu/
````cpp
class Solution {
public:
    double findMedianSortedArrays(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        int m = nums2.size();

        if (n > m)
            return findMedianSortedArrays(nums2, nums1);

        int LMax1, LMax2, RMin1, RMin2, c1, c2, low = 0, high = 2*n;

        while (low <= high) {
            c1 = (low + high) / 2;
            c2 = m + n - c1;

            LMax1 = (c1 == 0) ? INT_MIN : nums1[(c1 - 1) / 2];
            RMin1 = (c1 == 2*n) ? INT_MAX : nums1[c1 / 2];
            LMax2 = (c2 == 0) ? INT_MIN : nums2[(c2 - 1) / 2];
            RMin2 = (c2 == 2*m) ? INT_MAX : nums2[c2 / 2];

            if (LMax1 > RMin2)
                high = c1 - 1;
            else if (LMax2 > RMin1)
                low = c1 + 1;
            else
                break;
        }
        return (max(LMax1, LMax2) + min(RMin1, RMin2))/2.0;
    }
};
````
