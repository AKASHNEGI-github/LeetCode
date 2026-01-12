# Math

---
| Math |
| ---- |
| Minimum Time Visiting All Points |
---

- Minimum Time Visiting All Points
```c++
class Solution {
public:
    int minTimeToVisitAllPoints(vector<vector<int>>& points) 
    {
        int minTime = 0;
        for(int i=0 ; i<(points.size()-1) ; i++)
        {
            int dx = abs(points[i+1][0] - points[i][0]);
            int dy = abs(points[i+1][1] - points[i][1]);
            minTime = minTime + min(dx , dy) + abs(dx - dy); // minTime = diagonal_moves + remaining_moves = min(dx, dy) + |dx - dy|
        }
        return minTime;
    }
};
```

---
