# GRAPH

---
| Graph |
| ----- |
| Number of Islands |
| Max Area of Island |
| Rotting Oranges |
---

- Number of Islands
```c++
class Solution {
public:
    void dfs(int i , int j , vector<vector<bool>>& visited , vector<vector<char>>& grid , int& row , int& col)
    {
        if(i<0 || j<0 || i>=row || j>=col || grid[i][j] != '1' || visited[i][j] == true)
        {
            return;
        }
        visited[i][j] = true;
        dfs(i-1 , j , visited , grid , row , col); // Top
        dfs(i , j+1 , visited , grid , row , col); // Right
        dfs(i+1 , j , visited , grid , row , col); // Bottom
        dfs(i , j-1 , visited , grid , row , col); // Left
    }

    int numIslands(vector<vector<char>>& grid) 
    {
        int countIslands = 0;
        int row = grid.size();
        int col = grid[0].size();
        vector<vector<bool>> visited(row , vector<bool>(col , false));
        for(int i=0 ; i<row ; i++)
        {
            for(int j=0 ; j<col ; j++)
            {
                if(grid[i][j] == '1' && visited[i][j] == false)
                {
                    dfs(i , j , visited , grid , row , col);
                    countIslands++;
                }
            }
        }
        return countIslands;
    }
};
```

- Max Area of Island
```c++
class Solution {
public:
    void dfs(int i , int j , vector<vector<bool>>& visited , vector<vector<int>>& grid , int& row , int& col , int& area)
    {
        if(i<0 || j<0 || i>=row || j>=col || grid[i][j] != 1 || visited[i][j] == true)
        {
            return;
        }
        area = area + 1;
        visited[i][j] = true;
        dfs(i-1 , j , visited , grid , row , col , area); // Top
        dfs(i , j+1 , visited , grid , row , col , area); // Right
        dfs(i+1 , j , visited , grid , row , col , area); // Bottom
        dfs(i , j-1 , visited , grid , row , col , area); // Left
    }

    int maxAreaOfIsland(vector<vector<int>>& grid) 
    {
        int maxArea = 0;
        int row = grid.size();
        int col = grid[0].size();
        vector<vector<bool>> visited(row , vector<bool>(col , false));
        for(int i=0 ; i<row ; i++) 
        {
            for(int j=0 ; j<col ; j++) 
            {
                if(grid[i][j] == 1 && visited[i][j] == false) 
                {
                    int area = 0;
                    dfs(i , j , visited , grid , row , col , area);
                    maxArea = max(area , maxArea);
                }
            }
        }
        return maxArea;
    }
};
```

- Rotting Oranges
```c++
class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid)
    {
        int ans = 0;
        int row = grid.size();
        int col = grid[0].size();
        queue<pair<pair<int , int> , int>> q;
        vector<vector<bool>> visited(row , vector<bool>(col , false));
        for(int i=0 ; i<row ; i++)
        {
            for(int j=0 ; j<col ; j++)
            {
                if(grid[i][j] == 2)
                {
                    q.push({{i , j} , 0});
                    visited[i][j] = true;
                }
            }
        }
        while(!q.empty())
        {
            int i = q.front().first.first;
            int j = q.front().first.second;
            int time = q.front().second;
            q.pop();
            ans = max(time , ans);
            if((i-1) >= 0 && visited[i-1][j] == false && grid[i-1][j] == 1) // Top
            { 
                q.push({{i-1 , j} , time+1});
                visited[i-1][j] = true;
            }
            if((j+1) < col && visited[i][j+1] == false && grid[i][j+1] == 1) // Right
            { 
                q.push({{i , j+1} , time+1});
                visited[i][j+1] = true;
            }
            if((i+1) < row && visited[i+1][j] == false && grid[i+1][j] == 1) // Bottom
            { 
                q.push({{i+1 , j} , time+1});
                visited[i+1][j] = true;
            }
            if((j-1) >= 0 && visited[i][j-1] == false && grid[i][j-1] == 1) // Left
            { 
                q.push({{i , j-1} , time+1});
                visited[i][j-1] = true;
            }
        }
        for(int i=0 ; i<row ; i++)
        {
            for(int j=0 ; j<col ; j++)
            {
                if(grid[i][j] == 1 && visited[i][j] == false)
                {
                    return -1;
                }
            }
        }
        return ans;
    }
};
```


---
