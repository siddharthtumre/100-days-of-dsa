---
title: "Day 24"
date: "2022-07-02"
---

[Permutations](https://leetcode.com/problems/permutations/)

Given an array `nums` of distinct integers, return _all the possible permutations_. You can return the answer in **any order**.

```cpp
class Solution {
public:
    vector<vector<int>> ans;

	void solve(vector<int>& nums, int index){
        if (index == nums.size()) {
        ans.push_back(nums);
        return;
      }
      for (int i = index; i < nums.size(); i++) {
        swap(nums[index], nums[i]);
        solve(nums, index+1);
        swap(nums[index], nums[i]);
      }
    }
	
    void solveRec(vector<int>& nums, vector<int>& temp, vector<int>& freq){
        if(temp.size() == nums.size()){
            ans.push_back(temp);
            return;
            }
            
            for(int i=0; i<nums.size(); i++){
                if(!freq[i]){
                    temp.push_back(nums[i]);
                    freq[i] = 1;
                    solve(nums, temp, freq);
                    freq[i] = 0;
                    temp.pop_back();
                }
            }
        }
    vector<vector<int>> permute(vector<int>& nums) {
        int n = nums.size();
        // vector<int> temp;
        // vector<int> freq(n,0);
        // solve(nums, temp, freq);

		solve(nums, 0);
        
        return ans;
    }
};
```

[ Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/)

```cpp
class Solution {
public:
    
    bool solve(vector<int>& nums, int sum, int index, vector<vector<int>>& dp){
        if(sum==0){
            return true;
        }

        if(index<0){
            return false;
        }
        
        if(dp[index][sum]!=-1){
            return dp[index][sum];
        }
        
        bool take = false;
        if(sum-nums[index] >= 0){
            take = solve(nums, sum-nums[index], index-1, dp);
        }
        
        bool notTake = solve(nums, sum, index-1, dp);
        
        dp[index][sum] = take|notTake;
        
        return dp[index][sum];
        
        
    }
    
    bool solveTab(vector<int>& nums, int k){
        int n=nums.size();
        vector<vector<bool>> dp(n, vector<bool>(k+1, 0));
        for(int i=0; i<n; i++) dp[i][0] = true;
        if(nums[0]<=k)
            dp[0][nums[0]] = true;
        
        for(int i=1; i<n; i++){
            for(int target=1; target<=k; target++){
                 bool take = false;
                if(target-nums[i] >= 0){
                    take = dp[i-1][target-nums[i]];
                }

                bool notTake = dp[i-1][target];

                dp[i][target] = take|notTake;

            }
        }
        return dp[n-1][k];
        
    }
    
    bool canPartition(vector<int>& nums) {
        int n = nums.size();
        int s = accumulate(nums.begin(), nums.end(), 0);
        
        if(s%2 != 0){
            return false;
        }
        
        int k = s/2;
//         vector<vector<int>>dp(n, vector<int>(k+1, -1));
        
//         return solve(nums, k, n-1, dp);
        
        return solveTab(nums, k);
    }
};
```