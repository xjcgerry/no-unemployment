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
## 回溯算法
解决一个回溯问题，实际是一个决策树的遍历过程，需要思考三个问题：
* 路径：已做出的选择
* 选择列表：当前可以做出的选择
* 结束条件：也就是到达决策树底层，无法再做选择的条件。
回溯算法的框架：
````python
result = []
def backtrack(路径, 选择列表):
    if 满足结束条件:
        result.add(路径)
        return
    
    for 选择 in 选择列表:
        做选择
        backtrack(路径, 选择列表)
        撤销选择
````
所以本题的答案如下
````cpp
class Solution {
public:
    vector<vector<int>> result;

    void backtrack(vector<int> &nums, vector<int> &track) {
        if(track.size() == nums.size()) {
            result.push_back(track);
            return;
        }
        for (int i = 0; i < nums.size(); i++) {
            if (find(track.begin(), track.end(), nums[i]) != track.end())   //find函数，如果没有找到，就返回nums尾部的迭代器。否则就是找到了
                continue;
            track.push_back(nums[i]);
            backtrack(nums, track);
            track.pop_back();
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        vector<int> track;
        backtrack(nums, track);
        return result;
    }
};
````
