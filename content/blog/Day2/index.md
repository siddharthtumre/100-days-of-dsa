---
title: "Day 2 - Hashing"
date: "2022-06-10"
---

Hashing is a technique for storing and retrieving data as fast as possible. We use a hash function to generate the hash of a value, which is transformation of a large number to a small key. This small key is used as index in the hash table.

#### What is a good hash function?
- Computed hash value should not be able to convert back to original value.
- Should be easily computable.
- Should have less load factor which is given by number of elements/size of the table.
- The hash function should distribute keys uniformly.
- Minimize collisions.

#### Collision handling
1. [Separate Chaining](https://www.scaler.com/topics/data-structures/separate-chaining/) : Each cell of table is pointing to a linked list of keys that have same hash function value.
2. [Open addressing](https://www.scaler.com/topics/data-structures/open-addressing/): We use a prob number in the hash function which depends on the key which tells us the next available location in the hash table.
	- [Linear probing](https://www.scaler.com/topics/data-structures/open-addressing/#linear-probing), [quadratic probing](https://www.scaler.com/topics/data-structures/open-addressing/#quadratic-probing), [double hashing](https://www.scaler.com/topics/data-structures/double-hashing/) are types of open addressing.

### C++ STL Hashing 
|                | maps               | unordered maps                          |
| :------------  | :-----------       | :--------------                         |
| Ordering       | increasing         | unordered                               |
| Insertion      | O(log n)           | O(1)                                    |
| Accessing      | O(log n)           | O(1)                                    |
| Deletion       | O(log n)           | O(n)                                    |
| Implemented by | Red black trees    | hash tables(array of buckets)           |
| example syntax | map<int,int> mp;   | unordered_map<int,int> ump;             |

## Solved Problems
[2 Sum](https://www.interviewbit.com/problems/2-sum/)

Given an array of integers, find two numbers such that they add up to a specific target number.
- Approach
	- Use a map (mp) to store the indices of values in the array. Iterate using a for loop and if target-A[i] is present in the map then return `[mp[target-A[i]], i+1]` else if mp[A[i]] is not in the map (mp) then add `mp[A[i]] = i+1`

```cpp
vector<int> Solution::twoSum(const vector<int> &A, int B) {
    vector<int>ans;
    map<int,int>mp;
    for(int i=0;i<A.size();i++){
        if(mp.find(B-A[i]) != mp.end()){
            ans.push_back(mp[B-A[i]]);
            ans.push_back(i+1);
            return ans;
        }
        else if(mp.find(A[i]) == mp.end()){
            mp[A[i]] = i+1;
        }
    }
    return ans;
}
```

[Longest Consecutive Sequence](https://www.interviewbit.com/problems/longest-consecutive-sequence/)

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.
- Approach
	- Brute force - O(n<sup>3</sup>)
	- Hashing - O(n)

```cpp
int Solution::longestConsecutive(const vector<int> &A) {
    map<int,int>mp;
    for(int i=0; i<A.size(); i++){
        mp[A[i]] = 1; 
    }
    
    map<int,int> :: iterator it;
    int longest = 0;
    for(it=mp.begin(); it!=mp.end(); it++){
        if(mp.find(it->first-1) == mp.end()){
            int currentLong = 1;
            int currentNum = it->first;
            while(mp.find(currentNum+1) != mp.end()){
                currentNum++;
                currentLong++;
            }
            longest = max(longest, currentLong);
        }
        
    }
    return longest;
}
```

---
I solved only 2 questions on hashing today. But took part in a codechef contest - [June Long One 2022](https://www.codechef.com/JUNE221D?order=desc&sortBy=successful_submissions) under division 4. I was able to code up 6 questions out of 9 questions.

That's all for today!

> “Consistency is the hallmark of the unimaginative.”  
> ― Oscar Wilde



