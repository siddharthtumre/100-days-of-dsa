---
title: "Day 20 - Dynamic Programming"
date: "2022-06-28"
---

[Perfect Squares](https://leetcode.com/problems/perfect-squares/)

Given an integer `n`, return _the least number of perfect square numbers that sum to_ `n`.

A **perfect square** is an integer that is the square of an integer; in other words, it is the product of some integer with itself. For example, `1`, `4`, `9`, and `16` are perfect squares while `3` and `11` are not.

```cpp
int solve(int n){
	if(n==0)
		return 0;
	
	int ans = n;
	for(int i=1; i*i<=n; i++){
		ans = min(ans, 1+solve(n-(i*i)));
	}
	
	return ans;
}

int solveMem(int n, vector<int> &dp){
	if(n==0)
		return 0;
	if(dp[n]!=-1)
		return dp[n];
	
	int ans = n;
	for(int i=1; i*i<=n; i++){
		ans = min(ans, 1+solveMem(n-(i*i), dp));
	}
	
	dp[n] = ans;
	
	return dp[n];
}

int solveTab(int n){
	vector<int> dp(n+1, INT_MAX);
	
	dp[0] = 0;
	
	for(int i=1; i<=n; i++){
		for(int j=1; j*j<=n; j++){
			if(i-(j*j) >= 0)
				dp[i] = min(dp[i], 1+dp[i-(j*j)]);
		}
	}
	
	
	return dp[n];
}

int numSquares(int n) {
	// int ans = solve(n);
	
	// vector<int> dp(n+1, -1);
	// int ans = solveMem(n, dp);
	
	int ans = solveTab(n);
	
	return ans;
}
```

[Minimum Cost For Tickets](https://leetcode.com/problems/minimum-cost-for-tickets/)

You have planned some train traveling one year in advance. The days of the year in which you will travel are given as an integer array `days`. Each day is an integer from `1` to `365`.

Train tickets are sold in **three different ways**:

-   a **1-day** pass is sold for `costs[0]` dollars,
-   a **7-day** pass is sold for `costs[1]` dollars, and
-   a **30-day** pass is sold for `costs[2]` dollars.

The passes allow that many days of consecutive travel.

-   For example, if we get a **7-day** pass on day `2`, then we can travel for `7` days: `2`, `3`, `4`, `5`, `6`, `7`, and `8`.

Return _the minimum number of dollars you need to travel every day in the given list of days_.

```cpp
int solveRec(int n, vector<int>&days, vector<int>& cost, int index){
	if(index>=n){
		return 0;
	}

	int op1 = cost[0] + solveRec(n, days, cost, index+1);

	int i;
	for(i=index; i<n && days[i] < days[index]+7; i++);
	int op2 = cost[1] + solveRec(n, days, cost, i);

	for(i=index; i<n && days[i] < days[index]+30; i++);
	int op3 = cost[2] + solveRec(n, days, cost, i);

	return min(op1, min(op2,op3));
	
}

int solveMem(int n, vector<int>&days, vector<int>& cost, int index, vector<int>& dp){
	if(index>=n){
		return 0;
	}
	
	if(dp[index] != -1){
		return dp[index];
	}

	int op1 = cost[0] + solveMem(n, days, cost, index+1, dp);

	int i;
	for(i=index; i<n && days[i] < days[index]+7; i++);
	int op2 = cost[1] + solveMem(n, days, cost, i, dp);

	for(i=index; i<n && days[i] < days[index]+30; i++);
	int op3 = cost[2] + solveMem(n, days, cost, i, dp);

	dp[index] = min(op1, min(op2,op3));
	
	return dp[index];
	
}

int solveTab(int n, vector<int>&days, vector<int>& cost){
	vector<int>dp(n+1, INT_MAX);
	
	dp[n] = 0;
	
	for(int k=n-1; k>=0; k--){
		int op1 = cost[0] + dp[k+1];

		int i;
		for(i=k; i<n && days[i] < days[k]+7; i++);
		int op2 = cost[1] + dp[i];

		for(i=k; i<n && days[i] < days[k]+30; i++);
		int op3 = cost[2] + dp[i];

		dp[k] = min(op1, min(op2,op3));
	}
	
	return dp[0];
	
	
}

int mincostTickets(vector<int>& days, vector<int>& costs) {
	// int ans = solveRec(days.size(), days, costs, 0);
	
	// vector<int>dp(days.size()+1, -1);
	// int ans = solveMem(days.size(), days, costs, 0, dp);
	
	int ans = solveTab(days.size(), days, costs);
	return ans;
}
```