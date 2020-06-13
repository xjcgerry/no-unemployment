# 136. 只出现一次的数字
## 哈希
````cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        map<int, int> m;
        for (int i = 0; i < nums.size(); i++) {
            //看该数字是否第一次出现
            if (m[nums[i]] == 1)    //之前出现过一次了，删除该数字
                m.erase(nums[i]);
            else  //未出现过，value+1
                m[nums[i]]++;
        }
        return m.begin()->first;
    }
};
````

## 异或
````cpp
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int res = 0;
        for (auto num: nums) {
            res ^= num;
        }
        return res;
    }
};
````
