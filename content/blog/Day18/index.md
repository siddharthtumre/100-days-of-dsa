---
title: "Day 18 - 2D Dynamic Programming - 0/1 Knapsack"
date: "2022-06-26"
---

[0/1 Knapsack](https://www.codingninjas.com/codestudio/problems/0-1-knapsack_920542?topList=love-babbar-dsa-sheet-problems&leftPanelTab=1&utm_source=youtube&utm_medium=affiliate&utm_campaign=Lovebabbar)

The famous knapsack problem. You are packing for a vacation on the sea side and you are going to carry only one bag with capacity S. You also have N items that you might want to take with you to the sea side. Unfortunately you can not fit all of them in the knapsack so you will have to choose. For each item you are given its size and its value. You want to maximize the total value of all the items you are going to bring. What is this maximum total value?.  

**Input Format**

First line of input contains T - number of test cases. First line of each test case contains - S and N. N lines follow with two integers on each line describing one of your items. The first number is the size of the item and the next is the value of the item.

**Sample Input 0**
```
2
4 5
1 8
2 4
3 0
2 5
2 3
106 5
52 298
89 123
6 882
53 566
17 337
```

**Sample Output 0**
```
13
1785
```

Approach: For every item we decide whether we want to include an item or not  based on the condition that we have enough capacity in our bag. And for every item inluded we calculate the maximum total value that we can achieve.

**Time, Space Complexity:** O(items * capacity), O(capacity)

```cpp
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

// Recursion
int solve(vector<int> &weight, vector<int> &value, int index, int capacity){
    if(index==0){
        if(weight[0] <= capacity){
            return value[0];
        }
        else{
            return 0;
        }
    }
    
    int include=0;
    if(weight[index] <= capacity){
        include = value[index] + solve(weight, value, index-1, capacity-weight[index]);
    }
    int exclude = solve(weight, value, index-1, capacity);
    
    return max(include, exclude);
}

// Recursion + Memoization
int solveMem(vector<int> &weight, vector<int> &value, int index, int capacity, vector<vector<int>> &dp){
    if(index==0){
        if(weight[0] <= capacity){
            return value[0];
        }
        else{
            return 0;
        }
    }
    
    if(dp[index][capacity]!=-1){
        return dp[index][capacity];
    }
    
    int include=0;
    if(weight[index] <= capacity){
        include = value[index] + solveMem(weight, value, index-1, capacity-weight[index], dp);
    }
    int exclude = solveMem(weight, value, index-1, capacity, dp);
    
    dp[index][capacity] = max(include, exclude);
    
    return dp[index][capacity];
}

// Using Tabulation. Space used - O(items * capacity)
int solveTab(vector<int> &weight, vector<int> &value, int n, int capacity){
    
    vector<vector<int>>dp(n, vector<int>(capacity+1,0));
    
    for(int w=weight[0]; w<=capacity; w++){
        if(weight[0] <= capacity)
            dp[0][w] = value[0];
        else
            dp[0][w] = 0;
    }
    
    for(int index=1; index<n; index++){
        for(int w=0; w<=capacity; w++){
            int include = 0;
            if(weight[index]<=w){
                include = value[index] + dp[index-1][w-weight[index]];
            }
            int exclude = dp[index-1][w];
            
            dp[index][w] = max(include, exclude);
        }
    }
    
    return dp[n-1][capacity];
}

// Space optimized using O(2*capacity) space
int solveTabSO(vector<int> &weight, vector<int> &value, int n, int capacity){
    
    vector<int>prev(capacity+1, 0);
    vector<int>curr(capacity+1, 0); 
    
    for(int w=weight[0]; w<=capacity; w++){
        if(weight[0] <= capacity)
            prev[w] = value[0];
        else
            prev[w] = 0;
    }
    
    for(int index=1; index<n; index++){
        for(int w=0; w<=capacity; w++){
            int include = 0;
            if(weight[index]<=w){
                include = value[index] + prev[w-weight[index]];
            }
            int exclude = prev[w];
            
            curr[w] = max(include, exclude);
        }
        prev = curr;
    }
    
    return prev[capacity];
}

// Space optimized using only O(capacity) space
int solveTabSO2(vector<int> &weight, vector<int> &value, int n, int capacity){
    
    vector<int>curr(capacity+1, 0); 
    
    for(int w=weight[0]; w<=capacity; w++){
        if(weight[0] <= capacity)
            curr[w] = value[0];
        else
            curr[w] = 0;
    }
    
    for(int index=1; index<n; index++){
        for(int w=capacity; w>=0; w--){
            int include = 0;
            if(weight[index]<=w){
                include = value[index] + curr[w-weight[index]];
            }
            int exclude = curr[w];
            
            curr[w] = max(include, exclude);
        }
    }
    
    return curr[capacity];
}

int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int t;
    cin>>t;
    while(t--){
        int s,n;
        cin>>s>>n;
        vector<int>weight(n);
        vector<int>value(n);
        
        for(int i=0; i<n; i++){
            cin>>weight[i];
            cin>>value[i];
        }
        
        // int ans = solve(weight, value, n-1, s);
        
        // vector<vector<int>>dp(n, vector<int>(s+1, -1));
        // int ans = solveMem(weight, value, n-1, s, dp);
        
        // int ans = solveTab(weight, value, n, s);
        
        int ans = solveTabSO2(weight, value, n, s);
        
        cout<<ans<<endl;
    }
    return 0;
}
```
