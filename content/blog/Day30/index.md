---
title: "Day 30 - Graphs"
date: "2022-07-08"
---

[Cycle Detection In Undirected Graph using BFS](https://www.codingninjas.com/codestudio/problems/1062670?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website&leftPanelTab=0)

```cpp
#include<queue>
bool isCyclic(vector<int> adj[],vector<int> &vis,int v){
    vector<int> parent(vis.size(),-1);
    queue<int> q;
    q.push(v);
    vis[v] = true;
    
    while(!q.empty()){
        int val = q.front();
        q.pop();
        
        for(int i=0; i<adj[val].size(); i++){
            int temp = adj[val][i];
            if(!vis[temp]){
                q.push(temp);
                vis[temp] = true;
                parent[temp] = val;
            }else if(parent[val]!=temp){
                return true;
            }
        }
    }
    return false;
}

string cycleDetection (vector<vector<int>>& edges, int n, int m)

{
    // Write your code here.
    vector<int> adj[n+1];
    for(int i = 0;i<m;i++){
        adj[edges[i][0]].push_back(edges[i][1]);
        adj[edges[i][1]].push_back(edges[i][0]);
    }
    vector<int> vis(n+1,0);
    for(int i =1;i<=n;i++){
        if(!vis[i] && isCyclic(adj,vis,i)){
            return "Yes";
        }
    }
    return "No";

}
```

[Cycle Detection In Undirected Graph using DFS](https://www.codingninjas.com/codestudio/problems/1062670?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website&leftPanelTab=0)

```cpp
bool isCycle(int s, vector<vector<int>>& adj, vector<bool>& vis, int parent){
    vis[s] = true;
    
    for(int child: adj[s]){
        if(!vis[child]){
            if(isCycle(child, adj, vis, s))
                return true;
        }
        else if(child!=parent)
            return true;
    }
    return false;
}

string cycleDetection (vector<vector<int>>& edges, int n, int m)
{
    // Write your code here.
    vector<vector<int>> adj(n+1);
    
    for(int i=0; i<m; i++){
        adj[edges[i][0]].push_back(edges[i][1]);
        adj[edges[i][1]].push_back(edges[i][0]);
    }
    
    vector<bool>vis(n+1, false);
    
    for(int i=1; i<=n; i++){
        if(!vis[i] && isCycle(i, adj, vis, -1))
            return "Yes";
    }  
    return "No";  
}
```
