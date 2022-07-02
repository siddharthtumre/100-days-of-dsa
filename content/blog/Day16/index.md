---
title: "Day 16 - Dynamic Programming"
date: "2022-06-24"
---

[House Robber II](https://leetcode.com/problems/house-robber-ii/)
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed. All houses at this place are **arranged in a circle.** That means the first house is the neighbor of the last one. Meanwhile, adjacent houses have a security system connected, and **it will automatically contact the police if two adjacent houses were broken into on the same night**.

Given an integer array `nums` representing the amount of money of each house, return _the maximum amount of money you can rob tonight **without alerting the police**_.

Approach:
This problem is similar to [[Day15/index|Maximum sum of non adjacent elements]]. Only modification here is first and last house are adjacent. In order to consider this case we create 2 arrays, one excluding the first element and other excluding the last element. Then call the function to get maximum sum of non adjacecnt elements and return the maximum of answer returned from both arrays.

**Time, Space Complexity:** O(n), O(n)

```cpp
class Solution {
public:
    int solve(vector<int> &nums){
        int n = nums.size();
        int prev1 = nums[0];
        int prev2 = 0;
        for(int i=1; i<n; i++){
            int incl = prev2+nums[i];
            int excl = prev1;
            int ans = max(incl, excl);
            prev2 = prev1;
            prev1 = ans;
        }
        return prev1;
    }
    int rob(vector<int>& nums) {
        int n = nums.size();
        if(n==1){
            return nums[0];
        }
        vector<int>first;
        vector<int>second;
        
        for(int i=0; i<n; i++){
            if(i!=0){
                first.push_back(nums[i]);
            }
            if(i!=n-1){
                second.push_back(nums[i]);
            }
        }
        return max(solve(first), solve(second));
    }
};
```

[Cut Into Segments](https://www.codingninjas.com/codestudio/problems/cut-into-segments_1214651?topList=love-babbar-dsa-sheet-problems&leftPanelTab=0&utm_source=youtube&utm_medium=affiliate&utm_campaign=Lovebabbar)
You are given an integer ‘N’ denoting the length of the rod. You need to determine the maximum number of segments you can make of this rod provided that each segment should be of the length 'X', 'Y', or 'Z'.

Approach:
We try to determine maximum number of segments that can be formed by first considering the 'X' segment, 'Y' segment, 'Z' segment. We make a recursive call for each of these and return the maximum of these.

**Time, Space Complexity:** O(n), O(n)

```cpp
//Using recursion, without dp. It gives TLE
int solveRec(int n, int x, int y, int z){
    if(n==0){
        return 0;
    }
    if(n<0){
        return INT_MIN;
    }
    
    int a1 = solveRec(n-x, x, y, z)+1;
    int a2 = solveRec(n-y, x, y, z)+1;
    int a3 = solveRec(n-z, x, y, z)+1;
    
    return max(a1, max(a2,a3));
}

// Using Recuresion + Memoization
int solveMem(int n, int x, int y, int z, vector<int> &dp){
    if(n==0){
        return 0;
    }
    if(n<0){
        return INT_MIN;
    }
    
    if(dp[n]!=-1){
        return dp[n];
    }
    
    int a1 = solveMem(n-x, x, y, z, dp)+1;
    int a2 = solveMem(n-y, x, y, z, dp)+1;
    int a3 = solveMem(n-z, x, y, z, dp)+1;
    
    dp[n] = max(a1, max(a2,a3));
    return dp[n];
}

//Using Tablulation
int solveTab(int n, int x, int y, int z){
    vector<int>dp(n+1, -1);
    
    dp[0] = 0;
    for(int i=1; i<=n; i++){
        if(i-x>=0 && dp[i-x]!=-1){
            dp[i] = max(dp[i], dp[i-x]+1);
        }
        if(i-y>=0 && dp[i-y]!=-1){
            dp[i] = max(dp[i], dp[i-y]+1);
        }
        if(i-z>=0 && dp[i-z]!=-1){
            dp[i] = max(dp[i], dp[i-z]+1);
        }
    }
    
    if(dp[n] < 0)
        return 0;
    return dp[n];
}

int cutSegments(int n, int x, int y, int z) {
    // Write your code here.
//     int ans = solveRec(n,x,y,z);
//     if(ans<0)
//         return 0;
//     return ans;

//     vector<int> dp(n+1, -1);
//     int ans = solveMem(n, x, y, z, dp);
//     if(ans<0){
//         return 0;
//     }
//     return ans;
    
    int ans = solveTab(n, x, y, z);
    return ans;
}
```

