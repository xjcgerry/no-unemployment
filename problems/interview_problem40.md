# 面试题40. 最小的k个数
## 堆排序  
用一个大根堆实时维护数组的前k小值。首先将前k个数插入大根堆中，随后从第k+1个数开始遍历，如果当前遍历到的数比大根堆的堆顶的数要小，就把堆顶的数弹出，再插入当前遍历到的数。最后将大根堆里的数存入数组返回即可。  
在C++中，堆就是大根堆。  
priority_queue默认是大根堆，优先输出大数据。  
https://blog.csdn.net/weixin_36888577/article/details/79937886
````cpp
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        vector<int> vec(k,0);
        if (k == 0) return vec;
        priority_queue<int> Q;
        for (int i = 0; i < k; i++) Q.push(arr[i]);
        for (int i = k; i < (int)arr.size(); i++) {
            if (Q.top() > arr[i]) {
                Q.pop();
                Q.push(arr[i]);
            }
        }
        for (int i = 0; i < k; i++) {
            vec[i] = Q.top();
            Q.pop();
        }
        return vec;
    }
};
````
