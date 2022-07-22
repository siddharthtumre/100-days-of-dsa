---
title: "Day 33 - Graphs"
date: "2022-07-12"
---
[Number of Islands Easy](https://www.hackerrank.com/contests/smart-interviews/challenges/si-number-of-islands)

```cpp
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;

void dfs(int i, int j, vector<vector<int>>& grid){
    if(i<0 || j<0 || i>=int(grid.size()) || j>=int(grid[0].size()) || grid[i][j]!=1)
        return;

    grid[i][j]=2;
    dfs(i+1, j, grid);
    dfs(i, j+1, grid);
    dfs(i, j-1, grid);
    dfs(i-1, j, grid);
    dfs(i+1, j+1, grid);
    dfs(i+1, j-1, grid);
    dfs(i-1, j-1, grid);
    dfs(i-1, j+1, grid);
}

void solve(){
    int r,c;
    cin>>r>>c;
    
    vector<vector<int>>grid(r,vector<int>(c));
    
    for(int i=0;i<r;i++){
        string s;
        cin>>s;
        for(int j=0;j<c;j++){
            grid[i][j]=(s[j]-'0');
        }
    }
    
    int ans=0;
    for(int i=0;i<r;i++){
        for(int j=0;j<c;j++){
            if(grid[i][j]==1){
                dfs(i,j,grid);
                ans++;
            }
        }
    }
    cout<<ans<<endl;
}

int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int t;
    cin>>t;
    
    while(t--){
        solve();
    }
    return 0;
}
```

[Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)

```cpp
class Solution {
public:
    bool solve(vector<vector<int>>& graph, vector<int>& col, int s){
        col[s]=1;
        queue<int> q;
        q.push(s);
        
        while(!q.empty()){
            int temp=q.front();
            q.pop();
            for(int i : graph[temp]){
                if(col[i]==-1){
                    col[i]=1-col[temp];
                    q.push(i);
                }
                else if(col[i]==col[temp]){
                    return false;
                }
            }
        }
        
        return true;
    }
    bool isBipartite(vector<vector<int>>& graph) {
        int n = graph.size();
        
        vector<int>col(n,-1);
        
        for(int i=0; i<n; i++){
            if(col[i]==-1){
                if(!solve(graph,col,i)){
                    return false;
                }
            }
        }
        return true;
    }
};
```