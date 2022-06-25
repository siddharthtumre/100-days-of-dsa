---
title: "Day 12 - Stacks and Queues"
date: "2022-06-20"
---

[Queue Reversal](https://practice.geeksforgeeks.org/problems/queue-reversal/1)

```cpp
queue<int> rev(queue<int> q)
{
    // add code here.
    stack<int> st;
    while(!q.empty()){
        st.push(q.front());
        q.pop();
    }
    
    while(!st.empty()){
        q.push(st.top());
        st.pop();
    }
    return q;
}
```

Implement stack and queue using deque

```cpp
class Stack
{
    deque<int> dq;

public:
    void push(int value)
    {
        dq.push_back(value);
    }
    void pop()
    {
        dq.pop_back();
    }
    int top()
    {
        return dq.back();
    }
    bool isEmpty()
    {
        return (dq.size() > 0 ? true : false);
    }
};

class Queue
{
    deque<int> dq;

public:
    void enqueue(int value)
    {
        dq.push_back(value);
    }
    void dequeue()
    {
        dq.pop_front();
    }
    int front()
    {
        return dq.front();
    }
    bool isEmpty()
    {
        return (dq.size() > 0 ? true : false);
    }
};
```

[Reverse First K elements of Queue](https://practice.geeksforgeeks.org/problems/reverse-first-k-elements-of-queue/1)

```cpp
queue<int> modifyQueue(queue<int> q, int k) {
    stack<int>st;
    int d = q.size()-k;
    while(k--){
        st.push(q.front());
        q.pop();
    }
    while(!st.empty()){
        q.push(st.top());
        st.pop();
    }
    while(d--){
        q.push(q.front());
        q.pop();
    }
    return q;
}
```

[Online Stock Span](https://leetcode.com/problems/online-stock-span/)

```cpp
class StockSpanner {
    stack<pair<int,int>> st;
public:
    StockSpanner() {}
    
    int next(int price) {
        int c = 1;
    
        while(!st.empty() and price >= st.top().first){
            c += st.top().second;
            st.pop();
        }

        st.push({price, c});


        return st.top().second;
    }
};
```