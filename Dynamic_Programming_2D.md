# Dynamic Programming 2D
---

| Medium |
| ------ |
| Unique Paths |
| Unique Paths II |
| Minimum Path Sum |
| Maximum Non Negative Product in a Matrix |

---

### Medium

- Unique Paths
```c++
class Solution {
public:
    int uniquePathsRecursion(int i, int j, int m, int n) 
    {
        if(i == m-1 && j == n-1)
        {
            return 1;
        }
        if(i < 0 || i >= m || j < 0 || j >= n)
        {
            return 0;
        }
        int moveRight = uniquePathsRecursion(i, j+1, m, n);
        int moveDown = uniquePathsRecursion(i+1, j, m, n);
        int current = moveRight + moveDown;
        return current;
    }

    int uniquePaths(int m, int n) 
    {    
        int i = 0;
        int j = 0;
        int ans = uniquePathsRecursion(i, j, m, n);
        return ans;
    }
};
```

```c++
class Solution {
public:
    int uniquePathsMemoization(int i, int j, int m, int n, vector<vector<int>>& matrix) 
    {
        if(i == m-1 && j == n-1)
        {
            return 1;
        }
        if(i < 0 || i >= m || j < 0 || j >= n)
        {
            return 0;
        }
        if(matrix[i][j] == -1)
        {
            int moveRight = uniquePathsMemoization(i, j+1, m, n, matrix);
            int moveDown = uniquePathsMemoization(i+1, j, m, n, matrix);
            matrix[i][j] = moveRight + moveDown;
        }
        return matrix[i][j];
    }

    int uniquePaths(int m, int n) 
    {    
        vector<vector<int>> matrix(m+1, vector<int> (n+1, -1));
        int i = 0;
        int j = 0;
        int ans = uniquePathsMemoization(i, j, m, n, matrix);
        return ans;
    }
};
```

```c++
class Solution {
public:
    int uniquePaths(int m, int n) // Tabulation
    {    
        vector<vector<int>> matrix(m, vector<int> (n, -1));
        matrix[0][0] = 1;
        for(int row=1; row<m; row++)
        {
            matrix[row][0] = 1;
        }
        for(int col=1; col<n; col++)
        {
            matrix[0][col] = 1;
        }
        for(int i=1; i<m; i++)
        {
            for(int j=1; j<n; j++)
            {
                matrix[i][j] = matrix[i-1][j] + matrix[i][j-1];
            }
        }
        return matrix[m-1][n-1];
    }
};
```

- Unique Paths II
```c++
class Solution {
public:
    int uniquePathsWithObstaclesRecursuion(int i, int j, int& m, int& n, vector<vector<int>>& obstacleGrid)
    {
        if(i < 0 || i >= m || j < 0 || j >= n || obstacleGrid[i][j] == 1)
        {
            return 0;
        } 
        if(i == m-1 && j == n-1)
        {
            return 1;
        }   
        int moveRight = uniquePathsWithObstaclesRecursuion(i, j+1, m, n, obstacleGrid);
        int moveDown = uniquePathsWithObstaclesRecursuion(i+1, j, m, n, obstacleGrid);
        int current = moveRight + moveDown;
        return current;
    }

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) 
    {    
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        int i = 0;
        int j = 0;
        int ans = uniquePathsWithObstaclesRecursuion(i, j, m, n, obstacleGrid);
        return ans;
    }
};
```

```c++
class Solution {
public:
    int uniquePathsWithObstaclesMemoization(int i, int j, int& m, int& n, vector<vector<int>>& obstacleGrid, vector<vector<int>>& matrix)
    {
        if(i < 0 || i >= m || j < 0 || j >= n || obstacleGrid[i][j] == 1)
        {
            return 0;
        }   
        if(i == m-1 && j == n-1)
        {
            return 1;
        } 
        if(matrix[i][j] != 1)
        {
            int moveRight = uniquePathsWithObstaclesMemoization(i, j+1, m, n, obstacleGrid, matrix);
            int moveDown = uniquePathsWithObstaclesMemoization(i+1, j, m, n, obstacleGrid, matrix);
            matrix[i][j] = moveRight + moveDown;
        }
        return matrix[i][j];
    }

    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) 
    {    
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        int i = 0;
        int j = 0;
        vector<vector<int>> matrix(m+1, vector<int>(n+1, -1));
        int ans = uniquePathsWithObstaclesMemoization(i, j, m, n, obstacleGrid, matrix);
        return ans;
    }
};
```

```c++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) // Tabulation
    {    
        int m = obstacleGrid.size();
        int n = obstacleGrid[0].size();
        vector<vector<int>> matrix(m, vector<int>(n, 0));
        // Start Cell
        if (obstacleGrid[0][0] == 1) 
        {
            return 0;
        }
        matrix[0][0] = 1;
        // First Row
        for(int j = 1; j < n; j++) 
        {
            if(obstacleGrid[0][j] == 0)
            {
                matrix[0][j] = matrix[0][j-1];
            }
        }
        // First Column
        for(int i = 1; i < m; i++) 
        {
            if(obstacleGrid[i][0] == 0)
            {
                matrix[i][0] = matrix[i-1][0];
            }
        }
        // Rest Grid
        for(int i=1; i<m; i++)
        {
            for(int j=1; j<n; j++)
            {
                if(obstacleGrid[i][j] == 1)
                {
                    matrix[i][j] = 0;
                }
                else
                {
                    matrix[i][j] = matrix[i][j-1] + matrix[i-1][j];
                }
            }
        }
        return matrix[m-1][n-1];
    }
};
```

- Minimum Path Sum
```c++
class Solution {
public:
    int minPathSumRecursion(int i, int j, vector<vector<int>>& grid)
    {
        if(i >= grid.size() || j >= grid[0].size())
        {
            return INT_MAX;
        }
        if(i == grid.size()-1 && j == grid[0].size()-1)
        {
            return grid[i][j];
        }
        int moveRight = minPathSumRecursion(i, j+1, grid);
        int moveDown = minPathSumRecursion(i+1, j, grid);
        return grid[i][j] + min(moveRight, moveDown);
    }

    int minPathSum(vector<vector<int>>& grid) 
    {    
        int i = 0;
        int j = 0;
        int ans = minPathSumRecursion(i, j, grid);
        return ans;
    }
};
```

```c++
class Solution {
public:
    int minPathSumMemoization(int i, int j, vector<vector<int>>& grid, vector<vector<int>>& matrix)
    {
        if(i >= grid.size() || j >= grid[0].size())
        {
            return INT_MAX;
        }
        if(i == grid.size()-1 && j == grid[0].size()-1)
        {
            return grid[i][j];
        }
        if(matrix[i][j] == -1)
        {
            int moveRight = minPathSumMemoization(i, j+1, grid, matrix);
            int moveDown = minPathSumMemoization(i+1, j, grid, matrix);
            matrix[i][j] = grid[i][j] + min(moveRight, moveDown);
        }
        return matrix[i][j];
    }

    int minPathSum(vector<vector<int>>& grid) 
    {    
        int i = 0;
        int j = 0;
        int row = grid.size();
        int col = grid[0].size();
        vector<vector<int>> matrix(row+1, vector<int>(col+1, -1));
        int ans = minPathSumMemoization(i, j, grid, matrix);
        return ans;
    }
};
```

```c++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) // Tabulation
    {    
        int row = grid.size();
        int col = grid[0].size();
        vector<vector<int>> matrix(row, vector<int>(col, -1));
        matrix[0][0] = grid[0][0];
        // Calculate First Col
        for(int i=1; i<row; i++)
        {
            matrix[i][0] = grid[i][0] + matrix[i-1][0];
        }
        // Calculate First Row
        for(int j=1; j<col; j++)
        {
            matrix[0][j] = grid[0][j] + matrix[0][j-1];
        }
        // Calculate Matrix
        for(int i=1; i<row; i++)
        {
            for(int j=1; j<col; j++)
            {
                matrix[i][j] = grid[i][j] + min(matrix[i][j-1], matrix[i-1][j]);
            }
        }
        return matrix[row-1][col-1];
    }
};
```

- Maximum Non Negative Product in a Matrix
```c++
class Solution {
public:
    int modulo = 1e9 + 7;

    pair<long long, long long> maxProductPathRecursion(vector<vector<int>>& grid, int i, int j)
    {
        int row = grid.size();
        int col = grid[0].size();
        long long minValue = LLONG_MAX;
        long long maxValue = LLONG_MIN;
        // Base case
        if(i == row-1 && j == col-1)
        {
            return {grid[i][j], grid[i][j]};
        }
        // Move Right
        if(j+1 < col)
        {
            auto [minRight, maxRight] = maxProductPathRecursion(grid, i, j+1);
            minValue = min({minValue, grid[i][j] * maxRight, grid[i][j] * minRight});
            maxValue = max({maxValue, grid[i][j] * maxRight, grid[i][j] * minRight});
        }
        // Move Down
        if(i+1 < row)
        {
            auto [minDown, maxDown] = maxProductPathRecursion(grid, i+1, j);
            minValue = min({minValue, grid[i][j] * maxDown, grid[i][j] * minDown});
            maxValue = max({maxValue, grid[i][j] * maxDown, grid[i][j] * minDown});
        }
        return {minValue, maxValue};
    }

    int maxProductPath(vector<vector<int>>& grid) 
    {    
        auto [minProduct, maxProduct] = maxProductPathRecursion(grid, 0, 0);
        if(maxProduct >= 0)
        {
            return (maxProduct % modulo);
        }
        return -1;
    }
};
```

```c++
class Solution {
public:
    int modulo = 1e9 + 7;

    pair<long long, long long> maxProductPathMemoization(vector<vector<int>>& grid, int i, int j, vector<vector<pair<long long, long long>>>& matrix)
    {
        int row = grid.size();
        int col = grid[0].size();
        long long minValue = LLONG_MAX;
        long long maxValue = LLONG_MIN;
        // Base case
        if(i == row-1 && j == col-1)
        {
            return {grid[i][j], grid[i][j]};
        }
        // Already Calculated
        if(matrix[i][j] != make_pair(LLONG_MAX, LLONG_MIN))
        {
            return matrix[i][j];
        }
        // Move Right
        if(j+1 < col)
        {
            auto [minRight, maxRight] = maxProductPathMemoization(grid, i, j+1, matrix);
            minValue = min({minValue, grid[i][j] * maxRight, grid[i][j] * minRight});
            maxValue = max({maxValue, grid[i][j] * maxRight, grid[i][j] * minRight});
        }
        // Move Down
        if(i+1 < row)
        {
            auto [minDown, maxDown] = maxProductPathMemoization(grid, i+1, j, matrix);
            minValue = min({minValue, grid[i][j] * maxDown, grid[i][j] * minDown});
            maxValue = max({maxValue, grid[i][j] * maxDown, grid[i][j] * minDown});
        }
        // Store Result
        matrix[i][j] = {minValue, maxValue};
        return matrix[i][j];
    }

    int maxProductPath(vector<vector<int>>& grid) 
    {    
        int row = grid.size();
        int col = grid[0].size();
        vector<vector<pair<long long, long long>>> matrix(row, vector<pair<long long, long long>>(col, {LLONG_MAX, LLONG_MIN}));
        auto [minProduct, maxProduct] = maxProductPathMemoization(grid, 0, 0, matrix);
        if(maxProduct >= 0)
        {
            return (maxProduct % modulo);
        }
        return -1;
    }
};
```

```c++
class Solution {
public:
    int modulo = 1e9 + 7;

    int maxProductPath(vector<vector<int>>& grid) // Tabulation
    {    
        int row = grid.size();
        int col = grid[0].size();
        vector<vector<pair<long long, long long>>> matrix(row, vector<pair<long long, long long>>(col));
        matrix[0][0] = {grid[0][0], grid[0][0]};
        // calculate First Row
        for(int j=1; j<col; j++)
        {
            matrix[0][j].first = grid[0][j] * matrix[0][j-1].first; // minValue
            matrix[0][j].second = grid[0][j] * matrix[0][j-1].second; // maxValue
        }
        // calculate First Row
        for(int i=1; i<row; i++)
        {
            matrix[i][0].first = grid[i][0] * matrix[i-1][0].first; // minValue
            matrix[i][0].second = grid[i][0] * matrix[i-1][0].second; // maxValue
        }
        // calculate Matrix
        for(int i=1; i<row; i++)
        {
            for(int j=1; j<col; j++)
            {
                long long minUp = matrix[i-1][j].first;
                long long maxUp = matrix[i-1][j].second;
                long long minLeft = matrix[i][j-1].first;
                long long maxLeft = matrix[i][j-1].second;
                matrix[i][j].first = min({grid[i][j] * minUp, grid[i][j] * maxUp, grid[i][j] * minLeft, grid[i][j] * maxLeft});
                matrix[i][j].second = max({grid[i][j] * minUp, grid[i][j] * maxUp, grid[i][j] * minLeft, grid[i][j] * maxLeft});
            }
        }
        auto [minProduct, maxProduct] = matrix[row-1][col-1];
        if(maxProduct >= 0)
        {
            return (maxProduct % modulo);
        }
        return -1;
    }
};
```
