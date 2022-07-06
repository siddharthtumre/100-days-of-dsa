---
title: "Day 21 - Dynamic Programming"
date: "2022-06-29"
---

[Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/)

Given an integer array `nums`, return the length of the longest strictly increasing subsequence.

A **subsequence** is a sequence that can be derived from an array by deleting some or no elements without changing the order of the remaining elements. For example, `[3,6,2,7]` is a subsequence of the array `[0,3,1,6,2,2,7]`. 

```cpp
int lengthOfLIS(vector<int>& nums) {
	int n = nums.size(), dp[n]; 
	if(n==1)
		return 1;
	for(int i = 0; i<n ; ++i)
		dp[i] = 1;
	for(int i = 1; i<n; ++i){
		for(int j = i-1; j >= 0; j--){
			if(nums[i] > nums[j])
				dp[i] = max(dp[j] + 1, dp[i]);
		} 
	}
	
	int maxi = 0; 
	for(int i = 0; i<n; ++i) 
		maxi = max(maxi, dp[i]); 
	
	return maxi; 
}
```

[Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/)

Given an integer array `nums`, find a contiguous non-empty subarray within the array that has the largest product, and return _the product_.

The test cases are generated so that the answer will fit in a **32-bit** integer.

A **subarray** is a contiguous subsequence of the array.
```cpp
int maxProduct(vector<int>& nums) {
	int n = nums.size();
	int maxSoFar = nums[0];
	int minSoFar = nums[0];
	
	int ans = maxSoFar;
	
	for(int i=1; i<n; i++){
		int curr = nums[i];
		int tempMax = max(curr, max(maxSoFar * curr, minSoFar * curr));
		minSoFar = min(curr, min(maxSoFar * curr, minSoFar * curr));
		
		maxSoFar = tempMax;
		
		ans = max(ans, maxSoFar);
	}
	
	return ans;
}
```