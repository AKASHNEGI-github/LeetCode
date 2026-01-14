# Dynamic Programming

---
| Dynamic Programming |
| ------------------- |
| Fibonacci Number
---

- Fibonacci Number
```c++
class Solution {
public:
    int recursion(int n)
    {
        if(n == 0 || n == 1)
        {
            return n;
        }
        return fib(n-1) + fib(n-2);
    }

    int fib(int n)
    {
        return recursion(n);
    }
};
```

```c++
class Solution {
public:
    int memoization(vector<int>& dp , int n)
    {
        if(n == 0 || n ==1)
        {
            return n;
        }
        if(dp[n] == -1)
        {
            dp[n] = memoization(dp , n-1) + memoization(dp , n-2);
        }
        return dp[n];
    }

    int fib(int n) 
    {
        vector<int> dp(n+1 , -1);
        return memoization(dp , n);
    }
};
```

```c++
class Solution {
public:
    int tabulation(vector<int>& dp , int n)
    {
        if(n >= 0)
        {
            dp[0] = 0;
        }
        if(n >= 1)
        {
            dp[1] = 1;
        }
        for(int i=2 ; i<=n ; i++)
        {
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }

    int fib(int n) 
    {
        vector<int> dp(n+1 , -1);
        return tabulation(dp , n);
    }
};
```

```c++
class Solution {
public:
    int spaceOptimization(int n)
    {
        if(n == 0 || n == 1)
        {
            return n;
        }
        int ans = -1;
        int first = 0;
        int second = 1;
        for(int i=2 ; i<=n ; i++)
        {
            int current = first + second;
            ans = current;
            first = second;
            second = current;
        }
        return ans;
    }

    int fib(int n) 
    {
        return spaceOptimization(n);
    }
};
```

- Climbing Stairs
```c++
class Solution {
public:
    int climbStairs(int n) // Recursion
    {
        if(n == 0 || n == 1)
        {
            return 1;
        }
        return climbStairs(n-1) + climbStairs(n-2);
    }
};
```

```c++
class Solution {
public:
    int memoization(vector<int> dp , int n)
    {
        if(n == 0 || n == 1)
        {
            return 1;
        }
        if(dp[n] != -1)
        {
            return dp[n];
        }
        dp[n] = memoization(dp , n-1) + memoization(dp , n-2);
        return dp[n];
    }

    int climbStairs(int n) // Memoization(Top-Down)
    {
        vector<int> dp(n+1 , -1);
        return memoization(dp , n);
    }
};
```

```c++
class Solution {
public:
    int climbStairs(int n) // Tabulation(Bottom-Up)
    {
        vector<int> dp(n+1);
        dp[0] = 1;
        dp[1] = 1;
        for(int i=2 ; i<=n ; i++)
        {
            dp[i] = dp[i-1] + dp[i-2];
        }   
        return dp[n];
    }
};
```

```c++
class Solution {
public:
    int climbStairs(int n) // Space Optimization
    {
        int ans = 1;
        int first = 1;
        int second = 1;
        for(int i=2 ; i<=n ; i++)
        {
            int current = first + second;
            ans = current;
            first = second;
            second = current;
        }   
        return ans;
    }
};
```

- Min Cost Climbing Stairs
```c++
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) // Tabulation
    {
        int n = cost.size();
        vector<int> dp(n+1);
        dp[0] = cost[0];
        dp[1] = cost[1];
        for(int i=2 ; i<n ; i++)
        {
            dp[i] = cost[i] + min(dp[i-1] , dp[i-2]);
        }    
        return min(dp[n-1] , dp[n-2]);
    }
};
```

```c++
class Solution {
public:
    int minCostClimbingStairs(vector<int>& cost) // Space Optimization
    {
        int n = cost.size();
        int first = cost[0];
        int second = cost[1];
        for(int i=2 ; i<n ; i++)
        {
            int current = cost[i] + min(first , second);
            first = second;
            second = current;
        }    
        return min(first , second);
    }
};
```

- House Robber
```c++
class Solution {
public:
    int rob(vector<int>& nums) // Tabulation
    {
        int n = nums.size();
        vector<int> dp(n+1);
        dp[0] = 0;
        dp[1] = nums[0];
        for(int i=2 ; i<=n ; i++)
        {
            int value = nums[i-1];
            int include = dp[i-2] + value;
            int exclude = dp[i-1] + 0;
            dp[i] = max(include , exclude);
        }
        return dp[n];
    }
};
```

```c++
class Solution {
public:
    int rob(vector<int>& nums) // Space Optimization
    {
        int first = 0;
        int second = 0;
        int current = 0;
        for(int i=0 ; i<nums.size() ; i++)
        {
            int include = first + nums[i];
            int exclude = second + 0;
            current = max(include , exclude);
            first = second;
            second = current;
        }
        return current;
    }
};
```



---
