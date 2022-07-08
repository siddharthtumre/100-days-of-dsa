---
title: "Day 23 - Recursion (Striver SDE Sheet)"
date: "2022-07-01"
---

[Palindrome Partitioning](https://leetcode.com/problems/palindrome-partitioning/)

Given a string `s`, partition `s` such that every substring of the partition is a **palindrome**. Return all possible palindrome partitioning of `s`.

A **palindrome** string is a string that reads the same backward as forward.

```cpp
class Solution {
public:
    vector<vector<string>> ans;
    bool isPal(string s){
        int i=0, j = s.size()-1;
        while(i<=j){
            if(s[i++]!=s[j--]){
                return false;
            }
        }
        return true;
    }
    void solve(string s, int n, int index, vector<string> &temp){
        if(index==n){
            ans.push_back(temp);
            return;
        }
        
        int count = 1;
        
        for(int i = index; i<n; i++){
            string x = s.substr(index, count++);
            if(isPal(x)){
                temp.push_back(x);
                solve(s, n, i+1, temp);
                temp.pop_back();
            }
        }
    }
    vector<vector<string>> partition(string s) {
        int n = s.size();
        vector<string> temp;
        solve(s, n, 0, temp);
        
        return ans;
    }
};
```

[Permutation Sequence](https://leetcode.com/problems/permutation-sequence/)

```cpp
class Solution {
public:
    string getPermutation(int n, int k) {
        vector<int>num;
        int fact = 1;
        for(int i=1; i<n; i++){
            num.push_back(i);
            fact *= i;
        }
        num.push_back(n);
        
        string ans = "";
        k-=1;
        while(true){
            ans += to_string(num[k/fact]);
            num.erase(num.begin() + (k/fact));
            
            if(num.size()==0){
                break;
            }
            
            k = k%fact;
            fact = fact/num.size();
        }
        
        return ans;
        
    }
};
```