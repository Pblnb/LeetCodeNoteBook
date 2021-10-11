
## 题目地址(59. 螺旋矩阵 II)

https://leetcode-cn.com/problems/spiral-matrix-ii/

## 题目描述

```
给你一个正整数 n ，生成一个包含 1 到 n2 所有元素，且元素按顺时针顺序螺旋排列的 n x n 正方形矩阵 matrix 。

示例 1：

输入：n = 3
输出：[[1,2,3],[8,9,4],[7,6,5]]

示例 2：

输入：n = 1
输出：[[1]]

提示：

1 <= n <= 20
```

## 代码

- 语言支持：C++

C++ Code:

```c++

class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> res(n, vector<int>(n, 0));  // 初始化一个n行n列的元素值全为0的二维数组
        int left = 0, right = n - 1, up = 0, down = n - 1;
        int i = 0, j = 0, num = 1;  // i,j分别表示遍历中的行和列
        while(num <= n * n) {
            while(j <= right) {
                res[i][j] = num;
                num ++;
                j ++;
            }
            up ++;  //正向遍历一行完成
            j --;
            i++;
            while(i <= down) {
                res[i][j] = num;
                num ++;
                i ++;
            }
            right --;  //正向遍历一列完成
            i --;
            j --;
            while(j >= left) {
                res[i][j] = num;
                num ++;
                j --;
            }
            down --;  // 逆向遍历一行完成
            j ++;
            i --;
            while(i >= up) {
                res[i][j] = num;
                num ++;
                i --;
            }
            left ++;  // 逆向遍历一列完成
            i ++;
            j ++;
        }
        return res;
    }
};

```


**复杂度分析**

令 n 为所需的数组长度。

- 时间复杂度：$O(n)$
- 空间复杂度：$O(n)$

## 更优代码
**方法一：模拟**
```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        int maxNum = n * n;
        int curNum = 1;
        vector<vector<int>> matrix(n, vector<int>(n));
        int row = 0, column = 0;
        vector<vector<int>> directions = {{0, 1}, {1, 0}, {0, -1}, {-1, 0}};  // 右下左上
        int directionIndex = 0;
        while (curNum <= maxNum) {
            matrix[row][column] = curNum;
            curNum++;
            int nextRow = row + directions[directionIndex][0], nextColumn = column + directions[directionIndex][1];
            if (nextRow < 0 || nextRow >= n || nextColumn < 0 || nextColumn >= n || matrix[nextRow][nextColumn] != 0) {
                directionIndex = (directionIndex + 1) % 4;  // 顺时针旋转至下一个方向
            }
            row = row + directions[directionIndex][0];
            column = column + directions[directionIndex][1];
        }
        return matrix;
    }
};


```

**方法二:按层模拟**
```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        int num = 1;
        vector<vector<int>> matrix(n, vector<int>(n));
        int left = 0, right = n - 1, top = 0, bottom = n - 1;
        while (left <= right && top <= bottom) {
            for (int column = left; column <= right; column++) {
                matrix[top][column] = num;
                num++;
            }
            for (int row = top + 1; row <= bottom; row++) {
                matrix[row][right] = num;
                num++;
            }
            if (left < right && top < bottom) {
                for (int column = right - 1; column > left; column--) {
                    matrix[bottom][column] = num;
                    num++;
                }
                for (int row = bottom; row > top; row--) {
                    matrix[row][left] = num;
                    num++;
                }
            }
            left++;
            right--;
            top++;
            bottom--;
        }
        return matrix;
    }
};

```
