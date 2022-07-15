---
title: "Day 27 - Dynamic Programming"
date: "2022-07-05"
---

[Minimum Cost For Tickets](https://leetcode.com/problems/minimum-cost-for-tickets/)

Space optimized submission of the solution [[Day20/index|Minimum Cost for Tickets]] submitted on Day20.

```cpp
class Solution {
public:
    int mincostTickets(vector<int>& days, vector<int>& costs) {
        int ans=0;
    
        queue<pair<int,int>> month;
        queue<pair<int,int>> week;

        for(int day:days){

            // Remove expired days
            while(!month.empty() && month.front().first+30 <= day){
                month.pop();
            }

            while(!week.empty() && week.front().first+7 <= day){
                week.pop();
            }

            month.push(make_pair(day, ans+costs[2]));
            week.push(make_pair(day, ans+costs[1]));

            ans = min(ans+costs[0], min(month.front().second, week.front().second));
        }

        return ans;
    }
};
```

[Maximal Square](https://leetcode.com/problems/maximal-square/)

```cpp
class Solution {
public:
    int solve(vector<vector<char>>& a, int i, int j, int& maxi, vector<vector<int>>& dp){
        if(i>=a.size() || j>=a[0].size()){
            return 0;
        }
        
        if(dp[i][j]!=-1){
            return dp[i][j];
        }
        
        int right = solve(a, i, j+1, maxi, dp);
        int diag = solve(a, i+1, j+1, maxi, dp);
        int down = solve(a, i+1, j, maxi, dp);
        
        if(a[i][j]=='1'){
            dp[i][j] = 1+min(right, min(diag, down));
            maxi = max(dp[i][j], maxi);
            return dp[i][j];
        }else{
            return dp[i][j]=0;
        }
        
    }
    
    void solveTab(vector<vector<char>>& a, int& maxi){
        int r = a.size();
        int c = a[0].size();
        vector<vector<int>>dp(r+1, vector<int>(c+1, 0));
        
        for(int i=r-1; i>=0; i--){
            for(int j=c-1; j>=0; j--){
                int right = dp[i][j+1];
                int diag = dp[i+1][j+1];
                int down = dp[i+1][j];

                if(a[i][j]=='1'){
                    dp[i][j] = 1+min(right, min(diag, down));
                    maxi = max(dp[i][j], maxi);
                }
            }
        }
    }
    int maximalSquare(vector<vector<char>>& matrix) {
        // int maxi = 0;
        // int n = matrix.size();
        // int m = matrix[0].size();
        // vector<vector<int>>dp(n,vector<int>(m,-1));
        // solve(matrix, 0, 0, maxi, dp);
        // return maxi*maxi;
        
        int maxi=0;
        solveTab(matrix, maxi);
        
        return maxi*maxi;
    }
};
```