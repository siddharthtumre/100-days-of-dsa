---
title: "Day 32 - Graphs (Topological sorting)"
date: "2022-07-10"
---

[Topological sort using BFS](https://practice.geeksforgeeks.org/problems/topological-sort/1)

```cpp
vector<int> topoSort(int V, vector<int> adj[]) 
{
	// code here
	vector<int> inDegree(V,0);
	
	for(int i=0; i<V; i++){
		for(int v : adj[i]){
			inDegree[v]++;
		}
	}
	
	queue<int> q;
	
	for(int i=0; i<V; i++){
		if(inDegree[i]==0){
			q.push(i);
		}
	}
	
	vector<int>ans;
	
	while(!q.empty()){
		int temp = q.front();
		q.pop();
		
		ans.push_back(temp);
		
		for(int v : adj[temp]){
			inDegree[v]--;
			if(inDegree[v]==0){
				q.push(v);
			}
		}
	}
	
	return ans;
}
```

[Topological sort using DFS](https://practice.geeksforgeeks.org/problems/topological-sort/1)

```
void dfs(int s, vector<bool>& vis, vector<int> adj[], stack<int>& st){
	vis[s] = true;
	
	for(int v : adj[s]){
		if(!vis[v]){
			dfs(v, vis, adj, st);
		}
	}
	
	st.push(s);
}
//Function to return list containing vertices in Topological order. 
vector<int> topoSort(int V, vector<int> adj[]) 
{
	// code here
	vector<bool>vis(V,false);
	stack<int>st;
	
	for(int i=0; i<V; i++){
		if(!vis[i]){
			dfs(i, vis, adj, st);
		}
	}
	
	vector<int> ans;
	while(!st.empty()){
		ans.push_back(st.top());
		st.pop();
	}
	
	return ans;
}
```