# 删除排序数组的重复项
给定一个排序数组，你需要在 原地 删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在 原地 修改输入数组 并在使用 O(1) 额外空间的条件下完成。
## 示例
给定 nums = [0,0,1,1,1,2,2,3,3,4],

函数应该返回新的长度 5, 并且原数组 nums 的前五个元素被修改为 0, 1, 2, 3, 4。

你不需要考虑数组中超出新长度后面的元素。
## 解法1
双指针：分别定义两个指针i和j，如果i和j位置的元素相等，就把j向后移一位；如果不相等，就把i加1，并把j位置上的元素赋值到i位置上。
````cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.size() == 0)
            return 0;
        int len = nums.size();
        int i = 0;
        for (int j = 1; j < len; j++) {
            if (nums[i] != nums[j]) {
                i++;
                nums[i] = nums[j];
            }
        }
        return i + 1;
    }
};
````
## 解法2
暴力法，借助vector的erase函数
````cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int j = 0;
        for (int i = 1; i<nums.size(); i++){
            if (nums[i] == nums[i - 1]){
                i--;
                nums.erase(nums.begin() + i);
            }
        }
        return nums.size();
    }
};
````
