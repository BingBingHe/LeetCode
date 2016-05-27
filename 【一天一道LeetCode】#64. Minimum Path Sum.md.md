#<center>一天一道LeetCode</center>

>本系列文章已全部上传至我的github，地址：[ZeeCoder‘s Github](https://github.com/Zeecoders/LeetCode)

>欢迎大家关注我的新浪微博，[我的新浪微博](http://weibo.com/zc463717263?is_all=1)

>欢迎转载，转载请注明出处

##（一）题目


Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

##（二）解题

题目大意：求从m*n的矩阵的左上角走到右下角的所有路径中，路径上的值加起来最小的路径。

思路可以参考：[【一天一道LeetCode】#62. Unique Paths](http://blog.csdn.net/terence1212/article/details/51502144) &&[【一天一道LeetCode】#63. Unique Paths II](http://blog.csdn.net/terence1212/article/details/51504344)
```cpp
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int row = grid.size();
        int col = grid[0].size();
        vector<vector<int>> path = grid; //path纪录当前点到右下角点的路径和最小值
    ﻿    ﻿//对矩阵进行改造，可以避免考虑越界
        vector<int> temp(col,2147483647);
        path.push_back(temp);
        for(int i = 0 ; i < row ; i++)
        {
            path[i].push_back(2147483647);
        }
        
        for(int i = row-1 ; i >=0 ; i--)
            for(int j = col-1 ; j>=0;j--)
            {
                if (i==row-1&&j==col-1) continue;//终点直接跳过
                if(path[i][j] ==grid[i][j])
                {
                    path[i][j] +=min(path[i+1][j],path[i][j+1]);//每一点到终点的路径和最小值等一向下和向右走的最小值加上自身
                }
            }
﻿        return path[0][0];
    }
};
```



