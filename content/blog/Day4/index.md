---
title: "Day 4 - Striver SDE Sheet - Arrays"
date: "2022-06-12"
---
## Solved Problems
[Rotate Image](https://leetcode.com/problems/rotate-image/): You are given an `n x n` 2D `matrix` representing an image, rotate the image by **90** degrees (clockwise).
- Approach: Find the transpose of the matrix and reversing the rows will get us 90 degrees rotated matrix.
	- Time, space complexity: O(n<sup>2</sup>), O(1)

```cpp
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        int m = matrix[0].size();
        
        for(int i=0; i<n; i++){
            for(int j=0; j<i; j++){
                swap(matrix[i][j], matrix[j][i]);
            }
        }
        for(int i=0; i<n; i++){
            int start = 0;
            int end = m-1;
            while(start<end){
                swap(matrix[i][start++], matrix[i][end--]);
            }
        }
    }
};
```

[Merge Intervals](https://leetcode.com/problems/merge-intervals/) Given an array of `intervals` where `intervals[i] = [starti, endi]`, merge all overlapping intervals, and return _an array of the non-overlapping intervals that cover all the intervals in the input_.
- Approach: sort the array and compare elements at each index with next one and store the interval in a new array.
	- Time, space complexity: O(nlogn + n), O(n)

```cpp
class Solution {
public:
    vector<vector<int>> merge(vector<vector<int>>& intervals) {
        
        sort(intervals.begin(), intervals.end());
        vector < vector < int >> merged;
        for (int i = 0; i < intervals.size(); i++) {
            if (merged.empty() || merged.back()[1] < intervals[i][0]) {
              vector<int> v = {
                intervals[i][0],
                intervals[i][1]
              };
              merged.push_back(v);
            } else {
              merged.back()[1] = max(merged.back()[1], intervals[i][1]);
            }
          }

          return merged;
    }
};
```

[Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/): You are given two integer arrays `nums1` and `nums2`, sorted in **non-decreasing order**, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

**Merge** `nums1` and `nums2` into a single array sorted in **non-decreasing order**.

- Approach: Using pointers at location m, n, m+n-1 and comparing the elements.
	- Time, space complexity: O(m+n), O(1)

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int i = m-1;
        int j = n-1;
        int k = m+n-1;
        
        while(i>=0 and j>=0){
	        if(nums1[i]<nums2[j])
	        {
	            nums1[k--]=nums2[j--]; 
            }
            else
            {
                nums1[k--]=nums1[i--]; 
            }
        }
     while(j>=0) nums1[k--]=nums2[j--];
    }
};
```

[Find the Duplicate Number](https://leetcode.com/problems/find-the-duplicate-number/): Given an array of integers `nums` containing `n + 1` integers where each integer is in the range `[1, n]` inclusive.

There is only **one repeated number** in `nums`, return _this repeated number_.

- Approach: Keep the count of elements in `nums` and whenever count exceeds 1, return the element.
	- Time, space complexity: O(n), O(n+1)

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n = nums.size();
        vector<int>arr(n+1, 0);
        int ans;
        for(int i=0; i<n; i++){
            if(arr[nums[i]]==1){
                ans = nums[i];
                break;
            }
            else{
                arr[nums[i]]++;
            }
        }
        return ans;
    }
};
```

[Repeat and Missing Number Array](https://www.interviewbit.com/problems/repeat-and-missing-number-array/): You are given a read only array of n integers from 1 to n. Each integer appears exactly once except A which appears twice and B which is missing.

Return A and B.

- Approach: Keep the count of elements in the array and when count is greater than 1, it is repeating element and when count is 0 it is missing.
	- Time, space complexity: O(n), O(n+1)

```cpp
vector<int> Solution::repeatedNumber(const vector<int> &A) {
    int n = A.size();
    vector<int> ans(2);
    vector<int> arr(n+1, 0);
    
    for(int i=0; i<n; i++){
        arr[A[i]]++;
    }
    
    for(int i=0; i<arr.size(); i++){
        if(arr[i]>1){
            ans[0]=i;
        }
    }
    
    for(int i=0; i<arr.size(); i++){
        if(arr[i]==0){
            ans[1]=i;
        }
    }
    return ans;
}
```

