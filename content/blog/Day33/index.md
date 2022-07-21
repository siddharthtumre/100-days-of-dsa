---
title: "Day 33 - Graphs (Connected components)"
date: "2022-07-11"
---

[Given an undirected graph, you have to find the number of connected components in the graph](https://www.hackerrank.com/contests/smart-interviews/challenges/si-number-of-connected-components)

**Approach:** Run BFS on every un-visited vertex to get the number of connected components.

```cpp
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
#include <queue>
using namespace std;

void bfs(int s, vector<bool>& vis, vector<vector<int>>& adj){
    queue<int> q;
    q.push(s);
    vis[s]=true;
    
    while(!q.empty()){
        int temp = q.front();
        q.pop();
        
        for(int i=0; i<int(adj[temp].size()); i++){
            int v = adj[temp][i];
            if(!vis[v]){
                q.push(v);
                vis[v]=true;
            }
        }
    }
}

void solve(){
    int v, e;
    cin>>v>>e;
    vector<vector<int>>adj(v+1);
    
    for(int i=0; i<e; i++){
        int u,v;
        cin>>u>>v;
        
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    
    int ans = 0;
    
    vector<bool>vis(v+1, false);
    
    for(int i=1;i<=v;i++){
        if(!vis[i]){
            ans++;
            bfs(i, vis, adj);
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

- Another approach is to perform a DFS and increment the counter.

```cpp
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
#include <queue>
using namespace std;

void dfs(int s, vector<bool>& vis, vector<vector<int>>& adj){
    vis[s]=true;
    for(int v : adj[s]){
        if(!vis[v]){
            dfs(v,vis,adj);
        }
    }
}

void solve(){
    int v, e;
    cin>>v>>e;
    vector<vector<int>>adj(v+1);
    
    for(int i=0; i<e; i++){
        int u,v;
        cin>>u>>v;
        
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    
    int ans = 0;
    
    vector<bool>vis(v+1, false);
    
    for(int i=1;i<=v;i++){
        if(!vis[i]){
            ans++;
            dfs(i, vis, adj);
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