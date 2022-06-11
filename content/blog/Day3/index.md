---
title: "Day 3"
date: "2022-06-11"
---

I solved 3 questions related to hashing, one question from Leetcode's Biweekly contest and Daily Leetcoding challenge question.

## Solved Problems
[Longest Substring Without Repeat](https://www.interviewbit.com/problems/longest-substring-without-repeat/)

```cpp
int Solution::lengthOfLongestSubstring(string s) {
    int longest = 0;
        int prevSub = -1;
        for(int i=0;i<s.size();i++){
            int j = i-1;
            while(j>prevSub){
                if(s[i]==s[j]){
                    prevSub=j;
                    break;
                }
                j--;
            }
        longest = max(i-prevSub, longest);
        }
    return longest;
}
```

[Colorful Number](https://www.interviewbit.com/problems/colorful-number/)

```cpp
int Solution::colorful(int A) {
    string num = to_string(A);
    set<int> s;
    for(int i=0; i<num.size(); i++){
        int product = 1;
        for(int j=i; j<num.size(); j++){
            product = (int)(num[j] - '0') * product;
            if(s.find(product) == s.end()){
                s.insert(product);
            }else{
                return 0;
            }
        }
    }
    return 1;
}
```

[Window String](https://www.interviewbit.com/problems/window-string/)

```cpp
string Solution::minWindow(string A, string B) {
    int table[256] = {0};
    int count=0;
    for(int k=0; k<B.size(); k++){
        if(table[B[k]] == 0){
            count++;
        }
        table[B[k]]++;
    }
    int length = INT_MAX;
    
    int i=0, j=0;
    int minStart;
    while(j<A.size()){
        table[A[j]]--;
        if (table[A[j]] == 0)
            count--;
        if (count == 0) {
            while (count == 0) {
                if (length > j - i + 1) {
                    length = min(length, j - i + 1);
                    minStart = i;
                }
 
                table[A[i]]++;
                if (table[A[i]] > 0)
                    count++;
                i++;
            }
        }
        j++;
    }
    if (length != INT_MAX)
        return A.substr(minStart, length);
    else
        return "";
    
}
```

[Strong Password Checker II](https://leetcode.com/contest/biweekly-contest-80/problems/strong-password-checker-ii/)

```python
class Solution(object):
    def strongPasswordCheckerII(self, password):
        """
        :type password: str
        :rtype: bool
        """
        
        low = False
        up = False
        num = False
        length = False
        spe = False
        cont = True
        
        if len(password)>=8:
            length = True
            
        regex = re.compile('[-!@#$%^&*()+]')
        
        if(regex.search(password) != None):
            spe = True
            
        for i in range(len(password)):
            if password[i].islower():
                low = True
            if password[i].isupper():
                up = True
            if(password[i].isnumeric()):
                num = True
            
            if(i!=0 and password[i]==password[i-1]):
                cont = False
                
        if(low and up and num and length and spe and cont):
            return True
        else:
            return False
```

*This one seems to be really easy to do with python.* There must be a way to everything with regex. Need to learn how to create regex patterns 🙃

[Minimum Operations to Reduce X to Zero](https://leetcode.com/problems/minimum-operations-to-reduce-x-to-zero/)

```cpp
#include<bits/stdc++.h>
class Solution {
public:
    int minOperations(vector<int>& nums, int x) {
        int sum = 0, n = nums.size();
        for (int i : nums) sum += i;
        int target = sum - x;
        int curr_sum = 0, max_len = 0;
        int start_idx = 0;
        bool found = false;
        for (int end_idx = 0; end_idx < n; end_idx++) {
            curr_sum += nums[end_idx];
            while (start_idx <= end_idx && curr_sum > target) {
                curr_sum -= nums[start_idx];
                start_idx += 1;
            }
            if (curr_sum == target) {
                found = true;
                max_len = max(max_len, end_idx - start_idx + 1);
            }
        }
        return found ? n - max_len : -1;
    }
};
```

>“Consistency requires you to be as ignorant today as you were a year ago.”  
>― Bernard Berenson
