# 84. 柱状图中最大的矩形
## 思考
对于每一个i都计算当前的最大矩形，分别找出左右高度小于当前高度的位置，相减之后再减去1就是宽度。高度乘宽度就是面积。  
真的想不过来，到底是精神不集中，还是我就不是这块料呢o(╥﹏╥)o  
计算每一个柱子左右小于他高度的柱子的位置，用left_i和right_i记录下来。
````cpp
class Solution {
public:
    int largestRectangleArea(vector<int>& heights) {
        if (heights.size() == 0){
            return 0;
        }
        int n = heights.size();
        vector<int> left_i(n);
        vector<int> right_i(n);
        left_i[0] = -1;
        right_i[n-1] = n;
        int res = 0;
        for (int i = 1; i < n; i++){
            int tmp = i-1;
            while (tmp >= 0 && heights[tmp] >= heights[i]){ 如果左边的柱子比当前柱子更高
                tmp = left_i[tmp];    就把左边柱子的left_i值作为自己left_i值
            }
            left_i[i] = tmp;
        }
        for (int i = n-2; i >= 0; i--) {
            int tmp = i + 1;
            while (tmp < n && heights[tmp] >= heights[i]){
                tmp = right_i[tmp];
            }
            right_i[i] = tmp;
        }
        for (int i = 0; i < n; i++) {
            res = max(res, (right_i[i]-left_i[i]-1)*heights[i]);
        }
        return res;
    }
};
````
