# 57. 插入区间
给出一个无重叠的 ，按照区间起始端点排序的区间列表。  
在列表中插入一个新的区间，你需要确保列表中的区间仍然有序且不重叠（如果有必要的话，可以合并区间）。  
示例1：  
````
输入: intervals = [[1,3],[6,9]], newInterval = [2,5]
输出: [[1,5],[6,9]]
````
示例2：
````
输入: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
输出: [[1,2],[3,10],[12,16]]
解释: 这是因为新的区间 [4,8] 与 [3,5],[6,7],[8,10] 重叠。
````

## 思路
遍历原数组，如果当前区间在新区间的左边，就把当前区间保存入答案数组  
如果当前区间在新区间的右边，就把新区间保存进答案，当前区间和它之后的区间都保存进答案
在遍历过程中，如果有相交，应该更新新区间的左右边界

````cpp
class Solution {
public:
    vector<vector<int>> insert(vector<vector<int>>& intervals, vector<int>& newInterval) {
        vector<vector<int>> res;
        bool flag = false;
        for (int i = 0; i < intervals.size(); i++) {
            if (newInterval[0] > intervals[i][1]) { //新区间在当前区间右边
                res.push_back(intervals[i]);        //直接把当前区间存入答案
                continue;
            }
            if (newInterval[1] < intervals[i][0]) { //新区间在当前区间左边，后面的直接存入答案即可
                res.push_back(newInterval);         //新区间存入答案
                flag = !flag;
                for (;i < intervals.size(); i++)    //后面的区间都存入答案
                    res.push_back(intervals[i]);
                break;
            }
            //有交集，合并区间
            newInterval[0] = min(newInterval[0], intervals[i][0]);
            newInterval[1] = max(newInterval[1], intervals[i][1]);
        }
        if (!flag)
            res.push_back(newInterval);
        return res;
    }
};
````
