---
title: "Day 22 - Recursion (Striver SDE Sheet)"
date: "2022-06-30"
---

[Subset Sums](https://practice.geeksforgeeks.org/problems/subset-sums2234/1#)

Given a list **arr** of **N** integers, print sums of all subsets in it.

```cpp
void solve(vector<int> arr, int n, vector<int>& ans, int index, int sum){
	if(index==n){
		ans.push_back(sum);
		return;
	}
	sum+=arr[index];
	solve(arr, n, ans, index+1, sum);
	sum-=arr[index];
	solve(arr, n, ans, index+1, sum);
}
vector<int> subsetSums(vector<int> arr, int N)
{
	// Write Your Code here
	vector<int> ans;
	solve(arr, N, ans, 0, 0);
	
	return ans;
}
```

[Subsets II](https://leetcode.com/problems/subsets-ii/)

Given an integer array `nums` that may contain duplicates, return _all possible subsets (the power set)_.

The solution set **must not** contain duplicate subsets. Return the solution in **any order**.

```cpp
void solve(vector<int>& nums, int n, set<vector<int>>& ans, int index, vector<int> temp){
	if(index==n){
		ans.insert(temp);
		return;
	}
	temp.push_back(nums[index]);
	solve(nums, n, ans, index+1, temp);
	
	temp.pop_back();
	solve(nums, n, ans, index+1, temp);
}
vector<vector<int>> subsetsWithDup(vector<int>& nums) {
	sort(nums.begin(), nums.end());
	set<vector<int>> ans;
	vector<int> temp;
	solve(nums, ans, 0, temp);
	
	return vector<vector<int>>(ans.begin(), ans.end());
}
```

[Combination Sum](https://leetcode.com/problems/combination-sum/)

Given an array of **distinct** integers `candidates` and a target integer `target`, return _a list of all **unique combinations** of_ `candidates` _where the chosen numbers sum to_ `target`_._ You may return the combinations in **any order**.

The **same** number may be chosen from `candidates` an **unlimited number of times**. Two combinations are unique if the frequency of at least one of the chosen numbers is different.

It is **guaranteed** that the number of unique combinations that sum up to `target` is less than `150` combinations for the given input.

```cpp
int target;
    
vector<vector<int>> ans;

void solve(vector<int>& arr, int i, int sum, vector<int> op)
{ 
	if(i >= arr.size()) 
	{
		return;
	}
	
	if(arr[i] + sum == target)
	{
		op.push_back(arr[i]);
		ans.push_back(op);
		return;
	}
	
	if(arr[i] + sum < target)
	{
		vector<int> op1 = op;
		vector<int> op2 = op;
		
		op2.push_back(arr[i]);
		solve(arr, i, sum + arr[i], op2);
		solve(arr, i + 1, sum, op1);
	}
}

vector<vector<int>> combinationSum(vector<int>& arr, int required_target) {
	ans.clear();
	
	target = required_target;
	vector<int> op;
	sort(arr.begin(),arr.end());
	solve(arr, 0, 0, op); 
	
	return ans;
}
```

[Combination Sum II](https://leetcode.com/problems/combination-sum-ii/)

Given a collection of candidate numbers (`candidates`) and a target number (`target`), find all unique combinations in `candidates` where the candidate numbers sum to `target`.

Each number in `candidates` may only be used **once** in the combination.

**Note:** The solution set must not contain duplicate combinations.

```cpp
vector<vector<int>>ans;
void solve(vector<int>& arr, int i, int sum, int target, vector<int> op)
{ 
	if(i >= arr.size()) 
	{
		return;
	}
	
	if(arr[i] + sum == target)
	{
		op.push_back(arr[i]);
		ans.push_back(op);
		return;
	}
	
	if(arr[i] + sum < target)
	{   
		op.push_back(arr[i]);
		solve(arr, i + 1, sum + arr[i], target, op);
		op.pop_back();
	}
	while(i<(arr.size()-1) && arr[i] == arr[i+1]){
		i++;
	}
	solve(arr, i + 1, sum, target, op);
}
vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
	int n = candidates.size();
	
	sort(candidates.begin(), candidates.end());
	vector<int>op;
	solve(candidates, 0, 0, target, op);
	
	return ans;
}
```