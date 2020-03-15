# 42. 接雨水
## 按列来计算
对于每一列，左边最高的墙与右边最高的墙当中较矮的数值减去当前列的数值，就是该列能存下的水，≤0的不算。
````cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int sum = 0;
        int size = height.size();
        for (int i=1; i < size-1; i++){
            int max_left = 0;
            for (int j=i-1; j >= 0; j--){
                if (height[j]>max_left)
                    max_left = height[j];
            }
            int max_right = 0;
            for (int j = i; j < size; j++){
                if (height[j]>max_right)
                    max_right = height[j];                
            }
            int min_height = min(max_left, max_right);
            if (min_height > height[i])
                sum = sum + min_height-height[i];
        }
        return sum;
    }
};
````
## 动态规划  
https://leetcode-cn.com/problems/trapping-rain-water/solution/xiang-xi-tong-su-de-si-lu-fen-xi-duo-jie-fa-by-w-8/  
![avatar](http://baidu.com/pic/doge.png)
上面一种方法寻找每个下标左右最高的柱子时，会对柱子进行反复搜索导致复杂度升高。用两个数组max_left和max_right遍历一次得到结果。  
max_left[i]：它前边的墙的左边的最高高度和它前边的墙的高度选一个较大的，就是当前列左边最高的墙了。  
i=0，左边没有墙，max_left从i=1开始；i=size-1，右边没有墙，max_right从i=size-2开始。  
````cpp
class Solution {
public:
    int trap(vector<int>& height) {
        if (height.size()==0) return 0;
        int size = height.size();
        int sum = 0;
        vector<int> max_left(size);
        vector<int> max_right(size);
        max_left[0] = height[0];
        max_right[size-1] = height[size-1];
        for (int i=1; i < size-1; i++)
            max_left[i] = max(max_left[i-1], height[i-1]);  //它前边的墙的左边的最高高度和它前边的墙的高度选一个较大的，就是当前列左边最高的墙了。
        for (int i=size-2; i >=0; i--)
            max_right[i] = max(max_right[i+1], height[i+1]);
        for (int i = 1; i < size-1; i++)
        {
            int min_value = min(max_left[i], max_right[i]);
            if (min_value > height[i])
                sum = sum + (min_value - height[i]);
        }
        return sum;
    }
};
````
双指针法  
````cpp
class Solution {
public:
    int trap(vector<int>& height) {
        if (height.size() == 0) return 0;
        int size = height.size();
        int sum = 0;
        int max_left=0, max_right = 0;
        int left = 1;
        int right = size-2;
        for (int i=1; i < size-1; i++){
            //这种情况下，左边最高肯定小于右边最高，所以需要更新左边
            if (height[left-1] < height [right+1]){
                max_left = max(max_left, height[left-1]);
                int min_value = max_left;
                if (min_value > height[left]){
                    sum += (min_value- height[left]);
                }
                left++;
            } else {
                //左边最高大于等于右边最高了，需要更新右边，直到找到右边最高比左边最高大
                max_right = max(max_right, height[right+1]);
                int min_value = max_right;
                if (min_value > height[right])
                    sum += (min_value-height[right]);
                right--;
            }
        }
        return sum;
    }
};
````
