# 43. 旋转图象
两种做法。1、先转置，在每一行逆序；2、从外向内，每一圈处理，直到最里面
## 方法1
````cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int rows = matrix.size();
        int columns = matrix[0].size();

        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < i; j++) {
                swap(matrix[i][j], matrix[j][i]);
            }
        }
        for (int i = 0; i < rows; i++)
            reverse(matrix[i].begin(), matrix[i].end());
    }
};
````

## 方法2
每一层进行平移，平移时，每四个矩阵块作为一组进行旋转  
![image](https://github.com/xjcgerry/no-unemployment/blob/master/images/48-1.png)  
![image](https://github.com/xjcgerry/no-unemployment/blob/master/images/48-2.png)  
![image](https://github.com/xjcgerry/no-unemployment/blob/master/images/48-3.png)  
![image](https://github.com/xjcgerry/no-unemployment/blob/master/images/48-4.png)  
![image](https://github.com/xjcgerry/no-unemployment/blob/master/images/48-5.png)  
````cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int pos1 = 0, pos2 = matrix.size() - 1;
        while (pos1 < pos2) {
            int add = 0;
            while (add < pos2 - pos1) {
                int temp = matrix[pos2-add][pos1];
                matrix[pos2-add][pos1] = matrix[pos2][pos2-add];
                matrix[pos2][pos2-add] = matrix[pos1+add][pos2];
                matrix[pos1+add][pos2] = matrix[pos1][pos1+add];
                matrix[pos1][pos1+add] = temp;
                add = add + 1;
            }
            pos1 = pos1 + 1;
            pos2 = pos2 - 1;
        }
    }
};
````
