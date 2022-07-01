---
title: "Day 15 - Dynamic Programming"
date: "2022-06-23"
---

[Min Cost Climbing Stairs](https://leetcode.com/problems/min-cost-climbing-stairs/)

```cpp
int solve(vector<int> &cost, int n){
	vector<int> dp(n, -1);
	dp[0] = cost[0];
	dp[1] = cost[1];
	
	for(int i=2; i<n; i++){
		dp[i] = cost[i] + min(dp[i-1], dp[i-2]);
	}
	
	return min(dp[n-1], dp[n-2]);
}

int minCostClimbingStairs(vector<int>& cost) {
	int n = cost.size();
	vector<int> dp(n+1, -1);
	
	int ans = solve(cost, n);
	return ans;
}
```

[Coin Change](https://leetcode.com/problems/coin-change/)

```cpp
int solveTab(vector<int> &coins, int amount){
	vector<int> dp(amount+1, INT_MAX);
	dp[0] = 0;
	
	for(int i=1; i<=amount; i++){
		for(int j=0; j<coins.size(); j++){
			if(i-coins[j]>=0 && dp[i-coins[j]]!=INT_MAX)
				dp[i] = min(dp[i], 1+dp[i-coins[j]]);
		}
	}
	
	if(dp[amount] == INT_MAX){
		return -1;
	}
	
	return dp[amount];
}

int coinChange(vector<int>& coins, int amount) {
	int ans = solveTab(coins, amount);
	
	return ans;
}
```

[Max Sum Without Adjacent Elements](https://www.interviewbit.com/problems/max-sum-without-adjacent-elements/)

```cpp
int solve(vector<vector<int>> &A){
    int n = A[0].size();
    vector<int>dp(n);
    dp[0] = max(A[0][0], A[1][0]);
    dp[1] = max(dp[0], max(A[0][1], A[1][1]));
    
    for(int i=1; i<n; i++){
        int incl = dp[i-2] + max(A[0][i], A[1][i]);
        int excl = dp[i-1];
        dp[i] = max(incl, excl);
    }
    
    return dp[n-1];
}

int Solution::adjacent(vector<vector<int> > &A) {
    int n = A[0].size();
    int ans = solve(A);
    return ans;
}
```