---
title: "Day 13 - Problems"
date: "2022-06-21"
---

[Changing Directories](https://www.hackerrank.com/contests/smart-interviews/challenges/si-changing-directories)

```cpp
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;


int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        string curr="/";
        
        while(n--){
            string ip;
            cin>>ip;
            
            if(ip=="pwd"){
                cout<<curr<<endl;
            }
            
            if(ip=="cd"){
                string dir;
                cin>>dir;
                
                if(dir[0]=='/'){
                    curr=dir;
                }else{
                    curr=curr+dir;
                }
            }
            while(true){
                int k = curr.find('.');
                if(k==-1){
                    break;
                }
                
                string s1 = curr.substr(0, k-1);
                string s2 = curr.substr(k+2);
                k = s1.rfind('/');
                s1 = s1.substr(0,k);
                curr = s1+s2;
            }
        }
        cout<<endl;
    }
    return 0;
}
```

[Rectangular area under Histogram](https://www.hackerrank.com/contests/smart-interviews/challenges/si-rectangular-area-under-histogram/)

```cpp
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
#include <stack>
using namespace std;


int getMaxArea(vector<int> hist, int n)
{
    stack<int> s;
 
    int max_area = 0;
    int tp;
    int area_with_top;

    int i = 0;
    while (i < n)
    {
        if (s.empty() || hist[s.top()] <= hist[i])
            s.push(i++);
 
        else
        {
            tp = s.top();
            s.pop();
 
            area_with_top = hist[tp] * (s.empty() ? i :
                                   i - s.top() - 1);
 
            if (max_area < area_with_top)
                max_area = area_with_top;
        }
    }
 
    while (s.empty() == false)
    {
        tp = s.top();
        s.pop();
        area_with_top = hist[tp] * (s.empty() ? i :
                                i - s.top() - 1);
        
 
        if (max_area < area_with_top)
            max_area = area_with_top;
    }
 
    return max_area;
}

int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        vector<int> hist;
        for(int i=0; i<n; i++){
            int val;
            cin>>val;
            hist.push_back(val);
        }
        
        cout<<getMaxArea(hist, n)<<endl;
    }
    
    return 0;
}
```


