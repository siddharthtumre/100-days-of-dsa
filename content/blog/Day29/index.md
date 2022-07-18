---
title: "Day 29 - Graphs"
date: "2022-07-07"
---

[Course Schedule](https://leetcode.com/problems/course-schedule/)

There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses - 1`. You are given an array `prerequisites` where `prerequisites[i] = [ai, bi]` indicates that you **must** take course `bi` first if you want to take course `ai`.

-   For example, the pair `[0, 1]`, indicates that to take course `0` you have to first take course `1`.

Return `true` if you can finish all courses. Otherwise, return `false`.

**Example 1:**

**Input:** numCourses = 2, prerequisites = `[[1,0]]`
**Output:** true
**Explanation:** There are a total of 2 courses to take. 
To take course 1 you should have finished course 0. So it is possible.

**Example 2:**

**Input:** numCourses = 2, prerequisites = `[[1,0],[0,1]]`
**Output:** false
**Explanation:** There are a total of 2 courses to take. 
To take course 1 you should have finished course 0, and to take course 0 you should also have finished course 1. So it is impossible.

**Approach:** *Find if there is a cycle in directed graph using topological sort.*

```cpp
class Solution {
public:
     bool canFinish(int n, vector<vector<int>>& nums) {
    vector<int> indegree(n,0);
    vector<vector<int>> graph(n);
        for(auto x : nums){
            graph[x[0]].push_back(x[1]);
            indegree[x[1]]++;
        }
         
        list<int> q;
        vector<int> ans;
        for(int i=0;i<n;i++) if(indegree[i]==0) q.push_back(i);
        while(q.size()>0){
            int front  = q.front();
            q.pop_front();
            ans.push_back(front);
            for (int e : graph[front])
            {
                if (--indegree[e] == 0)
                    q.push_back(e);
            }
        }
        if(ans.size()==n) return true;
        return false;
    }
};
```
