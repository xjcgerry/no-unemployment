# 37. 解数独
## 思路
递归。让backtrack函数的返回值为bool，如果找到一个可行解就返回true，这样可以阻止后续的递归。
````cpp
class Solution {
public:
    void solveSudoku(vector<vector<char>>& board) {
        backtrack(board, 0, 0);
    }
    bool backtrack(vector<vector<char>>& board, int i, int j) {
        // 穷举到最后一列的话就换到下一行重新开始。
        if (j == 9)
            return backtrack(board, i + 1, 0);

        // 找到一个可行解，触发 base case
        if (i == 9)
            return true;

        // 对每个位置进行穷举
        for (int r = i; r < 9; r++) {
            for (int c = j; c < 9; c++) {
                // 如果有预设数字，不用我们穷举
                if (board[r][c] != '.')
                    return backtrack(board, i, j + 1);

                for (char ch = '1'; ch <= '9'; ch++) {
                    // 如果遇到不合法的数字，就跳过
                    if (!isValid(board, r, c, ch))
                        continue;
                    board[r][c] = ch;

                    // 如果找到一个可行解，立即结束
                    if(backtrack(board, r, c + 1))
                        return true;
                    //回溯法的回退步骤
                    board[r][c] = '.';
                }
                // 穷举完 1~9，依然没有找到可行解，此路不通
                return false;
            }
        }
        return false;
    }
    bool isValid(vector<vector<char>>& board, int r, int c, char n) {
        for (int i = 0; i < 9; i++) {
            if (board[r][i] == n)
                return false;
            if (board[i][c] == n)
                return false;
            if (board[(r/3)*3 + i / 3][(c/3)*3 + i % 3] == n)
                return false;
        }
        return true;
    }
};
````

另一种解法  
首先记录每一行、每一列、每一个分块中1~9数字的使用情况，然后进行回溯。
````cpp
class Solution {
public:
    //行，列，小格内某数字是否已填标记
    bool visitRow[9][9] = { false };    //表示第几行是否出现了数字1~9中的数，出现过就是true，没出现过就是false
    bool visitCol[9][9] = { false };
    bool visitBox[9][9] = { false };
    int num = 0;
    void solveSudoku(vector<vector<char>>& board) {
        //先遍历数独，记录表格中的初始状态
        for(int i = 0; i < 9; i++){
            for(int j = 0; j < 9; j++){
                if(board[i][j] != '.'){
                    visitRow[i][ board[i][j] - '1'] = true;
                    visitCol[j][ board[i][j] - '1'] = true;
                    visitBox[ (i / 3) * 3 + j / 3 ][ board[i][j] - '1'] = true;
                }
            }
        }
        backTrack(board, 0, 0);
    }
    bool backTrack(vector<vector<char>>& board, int row,int col){
        //找到需要填数字的坐标
        while(board[row][col] != '.'){
            if(++col >= 9){
                col = 0;
                row++;
            }
            //填满了
            if(row >= 9)
                return true;
        }
        for(int i = 0; i < 9; i++){     //对数字1~9循环
            int boxIndex = (row / 3) * 3 + col / 3; //分块的索引
            //已经填了
            if(visitRow[row][i] || visitCol[col][i] || visitBox[boxIndex][i])
                continue;
            board[row][col] = i + '1';  //因为是从0开始循环的，所以这里表示的是数字1可填
            visitRow[row][i] = true; visitCol[col][i] = true; visitBox[boxIndex][i] = true;
            if(backTrack(board, row, col)){
                return true;
            }
            else{
                //最后无法填满,回溯
                board[row][col] = '.';
                visitRow[row][i] = false; visitCol[col][i] = false; visitBox[boxIndex][i] = false;
            }
        }
        return false;
    }
};
````
