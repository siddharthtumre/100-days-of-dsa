---
title: "Day 25 - Subset Partitioning"
date: "2022-07-03"
---

[Matchsticks to Square](https://leetcode.com/problems/matchsticks-to-square/)

```cpp
class Solution {
public:
    
    bool solve(vector<int>& matchsticks,int i, vector<int>& sub){
        if(i==matchsticks.size()){
            for(int j=0; j<4; j++){
                if(sub[j]!=0){
                    return false;
                }
            }
            return true;
        }
        
        for(int j=0; j<4; j++){
            if(matchsticks[i]<=sub[j]){
                sub[j]-=matchsticks[i];
                if(solve(matchsticks,i+1,sub)) return true;
                sub[j]+=matchsticks[i];
            }
        }
		
        return false;
    }
    bool makesquare(vector<int>& matchsticks) {
        if(matchsticks.size()<4) return false;
        
		int sum = accumulate(matchsticks.begin(), matchsticks.end(),0);
        if(sum % 4 != 0) return false;
        
		int target=sum/4;
        vector<int>sub(4, target);
        
		sort(matchsticks.rbegin(), matchsticks.rend());
        
		return solve(matchsticks, 0, sub);
    }
};
```

[Partition to K Equal Sum Subsets](https://leetcode.com/problems/partition-to-k-equal-sum-subsets/)

```cpp
class Solution {
public:
    bool canPartitionKSubsets(vector<int>& nums, int k) {
        if(nums.size() == 0) {
            return false;
        }
        int sum =0 ;
        for(int i : nums) {
            sum += i;
        }
        int target = sum/k;
        vector<int> sub(k, 0);
        sort(nums.begin(), nums.end(), greater<int>());
        return solve(nums, sub, k, target, 0);
    }
    
    bool solve(vector<int>& nums, vector<int>& sub, int k, int target, int index) {
        
        if(index == nums.size()) {
            for(int i=1; i<sub.size(); i++) {
                if(sub[i] != sub[i-1]) {
                    return false;
                }
            }
            return true;
        }
        for(int i=0; i<k; i++) {
            if(sub[i]+nums[index] > target) {
                continue;
            }
            int j = i-1;
            while(j>=0) {
                if(sub[j] == sub[i]) {
                    break;
                }
                j--;
            }
            if(j != -1) {
                continue;
            }
            sub[i] += nums[index];
            if(solve(nums, sub, k, target, index+1)) {
                return true;
            }
            sub[i] -= nums[index];
        }
        return false;
    }
    
};
```
