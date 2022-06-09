---
title: "Day 1 of 100DaysOfDSA"
date: "2022-06-09"
---

Today I had been solving problems related to the two pointers concept. This technique is important if we want to find pairs which satisfy some condition in a sorted array.
## Solved Problems
[Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
- Approach:
	- Brute force - 2 for loops, O(n<sup>2</sup>)
	- Two pointers - O(n)

```
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        int i=0, j=numbers.size()-1;
        vector<int>ans(2);
        while(i<j){
            if(numbers[i]+numbers[j] == target){
                ans[0] = i+1;
                ans[1] = j+1;
                break;
            }
            else if(numbers[i]+numbers[j] < target){
                i++;
            }
            else{
                j--;
            }
        }
        return ans;
    }
};
```

[Diffk](https://www.interviewbit.com/problems/diffk/)
- Approach:
	- Brute force - 2 for loops, O(n<sup>2</sup>)
	- Two pointers - O(n)

```
int Solution::diffPossible(vector<int> &A, int B) {
    int i = 0, j = 1;
    while(i < A.size() && j < A.size())
    {
        if(i != j && A[j]-A[i] == B){
            return 1;
        }
        else if(A[j]-A[i] < B){
            j++;
        }
        else{
            i++;
        }
    }
    return 0;
}
```

[Intersection Of Sorted Arrays](https://www.interviewbit.com/problems/intersection-of-sorted-arrays/)
- Approach:
	- Brute force - O(n<sup>2</sup>)
	- Two Pointers - O(n+m)

```
vector<int> Solution::intersect(const vector<int> &A, const vector<int> &B) {
    int i=0, j=0;
    vector<int>ans;
    while(i<A.size() && j<B.size()){
        if(A[i]==B[j]){
            ans.push_back(A[i]);
            i++;
            j++;
        }
        else if(A[i]<B[j]){
            i++;
        }
        else{
            j++;
        }
    }
    return ans;
}
```

[Array 3 Pointers](https://www.interviewbit.com/problems/array-3-pointers/)
- Approach:
	- Brute force - O(n<sup>3</sup>)
	- Two pointers - O(n+m+p)

```
int Solution::minimize(const vector<int> &A, const vector<int> &B, const vector<int> &C) {
    int difference = INT_MAX;

    int i=0,j=0,k=0;
    while(i<A.size() and j<B.size() and k<C.size()){
        int temp = max(abs(A[i]-B[j]), max(abs(B[j]-C[k]), abs(C[k]-A[i])));
        if(temp<difference){
            difference = temp;
        }

        if(A[i] <= B[j] and A[i] <= C[k]){
            i++;
        }
		else if(B[j] <= A[i] and B[j] <= C[k]){
            j++;
        }
		else{
            k++;
        }
    }
    return difference;
}
```

[Container With Most Water](https://leetcode.com/problems/container-with-most-water/)
- Approach
	- Brute force - 2 for loops, O(n<sup>2</sup>)
	- Two pointers - O(n)

```
class Solution {
public:
    int maxArea(vector<int>& height) {
        int maximum = 0;
        int i=0, j=height.size()-1;
        while(i<j){
            int minHeight = min(height[i], height[j]);
            if(minHeight*(j-i) > maximum){
                maximum = minHeight*(j-i);
            }
            if(height[i]==height[j]){
                i++;
                j--;
            }
            if(minHeight == height[i]){
                i++;
            }
            if(minHeight==height[j]){
                j--;
            }
        }
        return maximum;
    }
};
```

[3Sum](https://leetcode.com/problems/3sum/)
- Approach
	- Brute force - 3 for loops, O(n<sup>3</sup>)
	- Fix one pointer in a for loop and then move other 2 pointers, O(n<sup>2</sup> + n)

```
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>>ans;
        
        sort(nums.begin(),nums.end());
        
        for(int i=0;i<nums.size();i++){
            if(i>0 and nums[i]==nums[i-1]){ // skip duplicates from left
                continue;
            }
            int j=i+1, k=nums.size()-1;
            
            while(j<k){
                if(nums[i]+nums[j]+nums[k]==0){
                    ans.push_back(vector<int>{nums[i], nums[j], nums[k]});
                    k--;
                    while(j<k and nums[k]==nums[k+1]){ //skip duplicates from the right
                        k--;
                    }
                }
                else if(nums[i]+nums[j]+nums[k]<0){
                    j++;
                }
                else{
                    k--;
                }
            }
        }
        return ans;
    }
};
```
