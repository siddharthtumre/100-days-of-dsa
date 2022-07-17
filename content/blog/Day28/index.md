---
title: "Day 28 - Graphs"
date: "2022-07-06"
---

[Clone Graph](https://leetcode.com/problems/clone-graph/)

```cpp
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> neighbors;
    Node() {
        val = 0;
        neighbors = vector<Node*>();
    }
    Node(int _val) {
        val = _val;
        neighbors = vector<Node*>();
    }
    Node(int _val, vector<Node*> _neighbors) {
        val = _val;
        neighbors = _neighbors;
    }
};
*/

class Solution {
public:
    Node* dfs(Node* curr, unordered_map<Node*, Node*>& mp){
        vector<Node*> arr;
        Node* clone = new Node(curr->val);
        mp[curr] = clone;
        
        for(auto it:curr->neighbors){
            if(mp.find(it)!=mp.end()){
                arr.push_back(mp[it]);
            }
            else{
                arr.push_back(dfs(it,mp));
            }
        }
        clone->neighbors=arr;
        
        return clone;
    }
    Node* cloneGraph(Node* node) {
        unordered_map<Node*, Node*> mp;
        
        if(node==NULL)
            return NULL;
        
        if(node->neighbors.size()==0){
            Node* clone = new Node(node->val);
            return clone;
        }
        
        return dfs(node, mp);
    }
};
```

[DFS of Graph](https://practice.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1)

```cpp
void dfsHelper(int n, vector<int> adj[], vector<bool>& vis, vector<int>& ans){
	vis[n] = true;
	ans.push_back(n);
	
	for(int i=0; i<adj[n].size(); i++){
		if(vis[adj[n][i]] != true){
			dfsHelper(adj[n][i], adj, vis, ans);
		}
	}
}
// Function to return a list containing the DFS traversal of the graph.
vector<int> dfsOfGraph(int V, vector<int> adj[]) {
	// Code here
	vector<bool>visited(V, false);
	vector<int>ans;
	
	dfsHelper(0, adj, visited, ans);
	return ans;
	
}
```

[BFS of graph](https://practice.geeksforgeeks.org/problems/bfs-traversal-of-graph/1)

```cpp
vector<int> bfsOfGraph(int V, vector<int> adj[]) {
	// Code here
	vector<int>ans;
	queue<int> q;
	
	vector<bool>visited(V, false);
	q.push(0);
	visited[0] = true;
	
	while(!q.empty()){
		int val = q.front();
		visited[val]=true;
		ans.push_back(val);
		
		for(int i=0; i<adj[val].size(); i++){
			if(visited[adj[val][i]]==false){
				q.push(adj[val][i]);
				visited[adj[val][i]]=true;
			}
		}
		q.pop();
	}
	
	return ans;
    }
```
