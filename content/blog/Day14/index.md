[Rain Water Trapped](https://www.interviewbit.com/problems/rain-water-trapped/)

```cpp
int Solution::trap(const vector<int> &A) {
    int n=A.size();
    vector<int> left(n);
    vector<int> right(n);
    
    left[0] = A[0];
    right[n-1] = A[n-1];
    
    for(int i=1; i<n; i++){
        left[i] = max(left[i-1], A[i]);
    }
    
    for(int i=n-2; i>=0; i--){
        right[i] = max(right[i+1], A[i]);
    }
    
    int sum = 0;
    
    for(int i=0; i<n; i++){
        sum += min(left[i],right[i]) - A[i];
    }
    return sum;
}
```

[Killing Dragons](https://www.hackerrank.com/contests/smart-interviews/challenges/si-killing-dragons)

```cpp
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
#include <queue>
using namespace std;


int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */   
    int t;
    cin>>t;
    while(t--){
        int n;
        cin>>n;
        
        vector<int> A(n);
        vector<int> B(n);
        for(int i=0; i<n; i++){
            cin>>A[i];
        }
        for(int i=0; i<n; i++){
            cin>>B[i];
        }

        vector<int> diff(n);
        int sum = 0;
        for(int i=0; i<n; i++){
            diff[i] = B[i]-A[i];
            sum+=diff[i];
        }
        
        if(sum<0){
            cout<<-1<<endl;
            continue;
        }
        
        sum = 0;
        int ans =0;
        
        
        for(int j=0; j<n; j++){
            sum+=diff[j];
            if(sum<0){
                sum = 0;
                ans = j+1;
            }
        }
        cout<<ans+1<<endl;
    }
    return 0;
}
```