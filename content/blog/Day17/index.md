---
title: "Day 17 - Dynamic Programming"
date: "2022-06-25"
---
[Count derangements](https://www.codingninjas.com/codestudio/problems/count-derangements_873861?leftPanelTab=0&utm_source=youtube&utm_medium=affiliate&utm_campaign=Lovebabbar)
A Derangement is a permutation of ‘N’ elements, such that no element appears in its original position. For example, an instance of derangement of {0, 1, 2, 3} is {2, 3, 1, 0}, because 2 present at index 0 is not at its initial position which is 2 and similarly for other elements of the sequence.

Given a number ‘N’, find the total number of derangements possible of a set of 'N’ elements.

Approach:
A number can be placed in `(n-1)` locations. So the solution would be `(n-1) * [solution of subproblems]`. If this number is swapped with some other number `i` then we need to solve for `(n-2)` subproblems, otherwise for `(n-1)` subproblems. So the equation becomes `dp[i] = (i-1) * (dp[i-1] + dp[i-2])`. 

**Time, space complexity:** O(n), O(1)

```cpp
#define MOD 1000000007
#include <vector>

// Recuresion + Memoization
long long int solveMem(int n, vector<long long int> &dp){
    if(n==1){
        return 0;
    }
    if(n==2){
        return 1;
    }
    if(dp[n] != -1){
        return dp[n];
    }
    
    dp[n] = (((n-1)%MOD) * ((solveMem(n-2, dp)%MOD) + (solveMem(n-1, dp)%MOD))%MOD);
    
    return dp[n];
}

// Tablulation
long long int solveTab(int n){
    vector<long long int> dp(n+1, -1);
    
    dp[1] = 0;
    dp[2] = 1;
    for(int i=3; i<=n; i++){
        dp[i] = (((i-1)%MOD) * (((dp[i-2] % MOD) + (dp[i-1] % MOD)) % MOD) % MOD);
    }
    
    return dp[n];
}

// Tabulation + space optimization
long long int solveTabSpaceOptimized(int n){
    
    long long int prev2 = 0;
    long long int prev1 = 1;
    for(int i=3; i<=n; i++){
        long long int ans = (((i-1)%MOD) * (((prev2 % MOD) + (prev1 % MOD)) % MOD) % MOD);
        prev2 = prev1;
        prev1 = dp[i];
    }
    
    return prev1;
}

long long int countDerangements(int n) {
    // Write your code here.
//     vector<long long int> dp(n+1, -1);
//     long long int ans = solveMem(n, dp);
//     return ans;
    
    long long int ans = solveTabSpaceOptimized(n);
    return ans;
}
```

```cpp
#define MOD 1000000007

int add(int a, int b){
    return (a%MOD + b%MOD)%MOD;
}
int mul(int a, int b){
    return ((a%MOD) * 1LL * (b%MOD))%MOD;
}
int solve(int n, int k){
    if(n==1){
        return k;
    }
    
    if(n==2){
        return k + (k*(k-1));
    }
    
    int ans = add((mul(solve(n-2, k), (k-1))), (mul(solve(n-1, k), (k-1))));
    return ans;
}

int solveMem(int n, int k, vector<int> &dp){
    if(n==1){
        return k;
    }
    
    if(n==2){
        return k + (k*(k-1));
    }
    if(dp[n] != -1){
        return dp[n];
    }
    
    dp[n] = add((mul(solveMem(n-2, k, dp), (k-1))), (mul(solveMem(n-1, k, dp), (k-1))));
    return dp[n];
}

int numberOfWays(int n, int k) {
    // Write your code here.
//     return solve(n,k);
    
    vector<int>dp(n+1, -1);
    return solveMem(n, k, dp);
}
```

[Ninja And The Fence](https://www.codingninjas.com/codestudio/problems/ninja-and-the-fence_3210208?topList=love-babbar-dsa-sheet-problems&leftPanelTab=0&utm_source=youtube&utm_medium=affiliate&utm_campaign=Lovebabbar)
Ninja has given a fence, and he gave a task to paint this fence. The fence has 'N' posts, and Ninja has 'K' colors. Ninja wants to paint the fence so that not more than two adjacent posts have the same color.

Ninja wonders how many ways are there to do the above task, so he asked for your help.

Your task is to find the number of ways Ninja can paint the fence.

Approach: If `n==1` it can be coloured in k ways. And for `n==2` it can be painted in `k + (k*(k-1))` ways. And further on either we can paint last 2 posts with same color or with different color. And these can be done in `k-1` ways. So the `dp` equation would become `dp[i] = (dp[i-1]*(k-1)) + (dp[i-2]*(k-1))`. 

**Time and Space complexity:** O(n), O(1)

```cpp
#define MOD 1000000007

int add(int a, int b){
    return (a%MOD + b%MOD)%MOD;
}
int mul(int a, int b){
    return ((a%MOD) * 1LL * (b%MOD))%MOD;
}

//Recursion - It will result in TLE
int solve(int n, int k){
    if(n==1){
        return k;
    }
    
    if(n==2){
        return k + (k*(k-1));
    }
    
    int ans = add((mul(solve(n-2, k), (k-1))), (mul(solve(n-1, k), (k-1))));
    return ans;
}


// Recursion + Memoization
int solveMem(int n, int k, vector<int> &dp){
    if(n==1){
        return k;
    }
    
    if(n==2){
        return k + (k*(k-1));
    }
    if(dp[n] != -1){
        return dp[n];
    }
    
    dp[n] = add((mul(solveMem(n-2, k, dp), (k-1))), (mul(solveMem(n-1, k, dp), (k-1))));
    return dp[n];
}

// Tabulation
int solveTab(int n, int k){
    vector<int>dp(n+1, -1);
    dp[1] = k;
    dp[2] = add(k, mul(k,k-1));
    
    for(int i=3; i<=n; i++){
        dp[i] = add(mul(dp[i-2], k-1), mul(dp[i-1], k-1));
    }
    
    return dp[n];
}

// Tabulation + Space Optimization
int solveTabSO(int n, int k){
    int prev2 = k;
    int prev1 = add(k, mul(k,k-1));
    
    for(int i=3; i<=n; i++){
        int ans = add(mul(prev2, k-1), mul(prev1, k-1));
        prev2 = prev1;
        prev1 = ans;
    }
    
    return prev1;
}

int numberOfWays(int n, int k) {
    // Write your code here.
//     return solve(n,k);
    
//     vector<int>dp(n+1, -1);
//     return solveMem(n, k, dp);
    
//     return solveTab(n, k);
    return solveTabSO(n,k);
}

```