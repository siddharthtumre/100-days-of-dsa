---
title: "Day 19 - Dynamic Programming"
date: "2022-06-27"
---

[Max Subarray Sum](https://www.hackerrank.com/contests/smart-interviews/challenges/si-max-subarray-sum/problem)
Given an array of integers, find the maximum subarray sum.  

**Input Format**
First line of input contains T - number of test cases. Its followed by 2T lines. First line of each test case contains N - size of the array and the second line contains N integers - elements of the array.

**Output Format**
For each test case, print the maximum subarray sum, followed by the start and end indices of the subarray, separated by newline. If multiple subarrays give the same sum, consider the lexicographically smaller one for the answer.

**Sample Input 0**
```
3
9
-24 0 28 28 55 -31 -27 -45 -24 
10
40 5 39 45 31 -44 73 -16 -31 27 
7
57 18 -14 17 31 16 -16
```

**Sample Output 0**
```
111 1 4
189 0 6
125 0 5
```

```cpp
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
#include <climits>
using namespace std;


void solve(vector<int> &a, int n){
    int start =0, end = 0, s=0;

    int dp[n];
    dp[0] =a[0];
    int ans = dp[0];
    for (int i = 1; i < n; i++){
        if(dp[i-1]>=0){
            dp[i] = dp[i-1] + a[i];
        }else{
            dp[i] = a[i];
            s = i;
        }
        if(ans<dp[i]){
            ans = dp[i];
            start = s;
            end = i;
        }
    }
    cout<<ans<<" "<<start<<" "<<end;
}

int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */  
    
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        
        vector<int> arr(n);
        
        for(int i=0; i<n; i++){
            cin>>arr[i];
        }
        
        solve(arr, n);
        cout<<endl;
    }
    return 0;
}
```

[Combination Sum IV](https://www.codingninjas.com/codestudio/problems/number-of-ways_3755252?leftPanelTab=0&utm_source=youtube&utm_medium=affiliate&utm_campaign=Lovebabbar)
You are given an array of distinct integers and you have to tell how many different ways of selecting the elements from the array are there such that the sum of chosen elements is equal to the target number tar.
```cpp
int solve(vector<int> &num, int tar){
    vector<int>dp(tar+1, 0);
        
    dp[0] = 1;
    for(int i=1; i<=tar; i++){
        for(int j=0; j<num.size(); j++){
            if(i-num[j] >= 0)
                dp[i] += dp[i-num[j]];
        }
    }
    return dp[tar];
}

int findWays(vector<int> &num, int tar)
{
    // Write your code here.
    int ans = solve(num, tar);
    return ans;
}
```