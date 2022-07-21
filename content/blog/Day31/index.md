---
title: "Day 31 - Graphs"
date: "2022-07-09"
---

[Detect Cycle In A Directed Graph](https://www.codingninjas.com/codestudio/problems/1062626?topList=striver-sde-sheet-problems&utm_source=striver&utm_medium=website)

You are given a directed graph having ‘N’ nodes. A matrix ‘EDGES’ of size M x 2 is given which represents the ‘M’ edges such that there is an edge directed from node `EDGES[i][0]` to node `EDGES[i][1]`.

Find whether the graph contains a cycle or not, return true if a cycle is present in the given directed graph else return false.

Approach: Here we use the depth-first-search to detect a cycle. To detect a cycle in a directed graph using breadth-first-search ([[Day29/index|link]]) can be done using topological sort.

```cpp
bool dfsCycle(int source, unordered_map<int,vector<int>> &adj, unordered_map<int,bool> &visited,unordered_map<int,bool> &dfsVisited){
    visited[source]=1;
    dfsVisited[source]=1;
    
    for(auto i:adj[source]){
        if(visited[i]==1 && dfsVisited[i]==1){
            return true;
        }
        else{
            bool CycleDetected=dfsCycle(i,adj,visited,dfsVisited);
            if(CycleDetected){
                return true;
            }
            
        }
    }
    dfsVisited[source]=0;
    return false;
    
}

int detectCycleInDirectedGraph(int n, vector < pair < int, int >> & edges) {
  unordered_map<int,vector<int>> adj;
    for(int i=0;i<n;++i){
        int u=edges[i].first;
        int v=edges[i].second;
        
        adj[u].push_back(v);
    }
    
    unordered_map<int,bool> visited;
    unordered_map<int,bool> dfsVisited;
    for(int i=0;i<n;++i){
        if(!visited[i]){
           bool ans = dfsCycle(i,adj,visited,dfsVisited);
           if(ans){
               return 1;
           }
        }
    }
    return 0;
}
```