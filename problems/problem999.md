# 999. 车的可用捕获量
首先遍历board找到车的位置。  
然后在四个方向移动寻找卒的位置。这里考的就是一个方向数组dx[4]、dy[4]。如果没有想到这一点的话，就分别在4个方向写for循环。
````cpp
class Solution {
public:
    int numRookCaptures(vector<vector<char>>& board) {
        int cnt = 0, st = 0, ed = 0;
        int dx[4] = {0, 1, 0, -1};
        int dy[4] = {1, 0, -1, 0};  //方向数组
        for (int i = 0; i < 8; i++) {
            for (int j = 0; j < 8; j++) {
                if (board[i][j] == 'R') {
                    st = i;
                    ed = j;
                    break;
                }
            }
        }

        for (int i = 0; i < 4; i++) {
            for (int step = 0; ; step++) {
                int tx = st + step * dx[i];
                int ty = ed + step * dy[i];
                if (tx < 0 || tx >= 8 || ty < 0 || ty >= 8 || board[tx][ty] == 'B') break;
                if (board[tx][ty] == 'p') {
                    cnt++;
                    break;
                }
            }
        }
        return cnt;

    }
};
````
