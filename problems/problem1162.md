# 1162. 地图分析
count_land 记录陆地的数量  
count_turn 记录搜索的轮数  
count_last_space 记录剩余海洋的数量

````cpp
class Solution {
public:
    int maxDistance(vector<vector<int>>& grid) {
        int N = grid.size();
        int count_land = 0;
        int count_turn = 0;
        int count_last_space;

        for (int i = 0; i < N; i++) {
            for (int j = 0; j < N; j++) {
                if (grid[i][j] == 1)
                    count_land++;
            }
        }

        if (count_land == N * N || count_land == 0) 
            return -1;
        
        count_last_space = N*N - count_land;
        while (count_last_space != 0) {
            count_turn++;
            for (int i = 0; i < N; i++) {
                for (int j = 0; j < N; j++) {
                    if (grid[i][j] == count_turn) {
                        if (i > 0 && grid[i-1][j] == 0) { //向左搜索
                            grid[i-1][j] = count_turn + 1;  //轮数加1
                            count_last_space--;
                        }
                        if (i < N-1 && grid[i+1][j] == 0) { //向右搜索
                            grid[i+1][j] = count_turn + 1;
                            count_last_space--;
                        }
                        if (j > 0 && grid[i][j-1] == 0) { //向下搜索
                            grid[i][j-1] = count_turn + 1;
                            count_last_space--;
                        }
                        if (j < N-1 && grid[i][j+1] == 0) { //向上搜索
                            grid[i][j+1] = count_turn + 1;
                            count_last_space--;
                        }
                    }
                }
            }
        }
        return count_turn;
    }
};
````
