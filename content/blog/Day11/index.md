---
title: "Day 11 - Stacks and Queues"
date: "2022-06-19"
---

##### Implement 2 stacks using one array
Create a data structure _twoStacks_ that represents two stacks. Implementation of _twoStacks_ should use only one array, i.e., both stacks should use the same array for storing elements.
- One approach is to divide the array into half and use them as 2 different stacks. It is not efficient when it comes to utilizing space.
- Another approach is to allow one stack to grow from the start and other from the end

```cpp
class twoStacks{
	int *arr;
	int size;
	int top1, top2;
	public:
		twoStacks(int n){
			size = n;
			arr = new int[n];
			top1 = -1;
			top2 = n;
		}
		void push1(int val){
			if(top1<top2-1){
				arr[++top1] = val;
			}else{
				cout<<"Overflow"<<endl;
			}
		}
		void push2(int val){
			if(top1<top2-1){
				arr[--top2] = val;
			}else{
				cout<<"Overflow"<<endl;
			}
		}
		int pop1(){
			if(top1>=0){
				return arr[top1--];
			}else{
				cout<<"Underflow"<<endl;
			}
		}
		int pop2(){
			if(top2<=size-1){
				return arr[top2++];
			}else{
				cout<<"Underflow"<<endl;
			}
		}
}
```

[Reverse the Sentence](https://www.hackerrank.com/contests/smart-interviews/challenges/si-reverse-the-sentence/submissions/code/1345978260)

```cpp
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;


string reverseSentence(string a){
    vector<string> tmp;
    string str = "";
    for (int i = 0; i < int(a.length()); i++)
    {
        if (a[i] == ' ')
        {
            tmp.push_back(str);
            str = "";
        }
        else
            str += a[i];
    }
   
    tmp.push_back(str);
    
    string ans="";
    for (int i = tmp.size() - 1; i >= 0; i--){
        ans+=tmp[i];
        ans+=" ";
    }
    return ans;
}

int main() {
    /* Enter your code here. Read input from STDIN. Print output to STDOUT */
    int t;
    cin>>t;
    while(t--){
        string a;
        getline(cin, a);
        while (a.length() == 0)
            getline(cin, a);
        
        cout<<reverseSentence(a)<<endl;
    }
    return 0;
}
```

[Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/)

```cpp
class MyStack {
public:
    queue<int> q;
    MyStack() {
        
    }
    
    void push(int x) {
        q.push(x);
        for(int i=0; i<q.size()-1; i++){
            q.push(q.front());
            q.pop();
        }
    }
    
    int pop() {
        int ans = q.front();
        q.pop();
        return ans;
    }
    
    int top() {
        return q.front();
    }
    
    bool empty() {
        return q.empty();
    }
};
```

[CMG - Collecting Mango](https://www.spoj.com/problems/CMG/)

```cpp
#include <iostream>
#include <cstdio>
#include <stack>

#define ll long long

using namespace std;

int main(){
    int t, c = 1;
    char ch;
    scanf("%d",&t);
    while (t--) {
        printf("Case %d:\n",c);
        ll n, max = 0, ip;
        stack<ll> mango;
        scanf("%lld",&n);
        
        while (n--) {
            scanf(" %c",&ch);
            switch (ch) {
                case 'A':
                    scanf("%lld",&ip);
                    if (ip > max)
                        max = ip;
                    mango.push(max);
                    break;
                    
                case 'Q':
                    if (mango.empty())
                      {max=0;
                      printf("Empty\n");}
                    else
                        printf("%lld\n",mango.top());
                    break;
                    
                case 'R':
                    if (!mango.empty())
                       { mango.pop();
                           if (!mango.empty())
                               {
                                   if(mango.top() < max)
                                       max = mango.top();
                               }
                               else max = 0;
                       }
                       break;
                default:
                    break;
            }
        }
        c++;
    }
    return 0;
}
```

