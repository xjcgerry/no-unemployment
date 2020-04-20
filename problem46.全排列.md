# 46. 全排列
## 思路
全排列问题，可以用dfs解决。  用的这个里面的解法：https://www.bilibili.com/video/BV1c7411h7EW  
dfs可以用来解决两类问题。permutation和combination。78题子集是combination问题。
````cpp
class Solution {
public:
    void dfs(vector<int>& nums, int pos, vector<int> &list, vector<vector<int>> &result, vector<int> &visited) {
        if(pos == nums.size()) {  //停止条件
            result.push_back(list);
            return;   //相当于break
        }
        for (int i = 0; i < nums.size(); i++) {
            if(!visited[i]) {
                list.push_back(nums[i]);
                visited[i] = 1;
                dfs(nums, pos + 1, list, result, visited);
                visited[i] = 0;   //回退
                list.pop_back();
            }
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        vector<vector<int>> result;
        vector<int> list;
        vector<int> visited(nums.size(),0);   //用来记录nums中的数是否被访问过
        dfs(nums, 0, list, result, visited);  //dfs的模板
        return result;
    }
};
````
