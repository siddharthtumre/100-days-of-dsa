---
title: "Day 7 - HackerRank Data Structures(Trees)"
date: "2022-06-15"
---

[Binary Search Tree : Insertion](https://www.hackerrank.com/challenges/binary-search-tree-insertion/problem)

```cpp
Node * insert(Node * root, int data) {
    if(root==NULL){
        return new Node(data);
    }
    
    if(data>root->data){
        root->right = insert(root->right, data);
    }else{
        root->left = insert(root->left, data);
    }

    return root;
}
```

[Tree: Huffman Decoding](https://www.hackerrank.com/challenges/tree-huffman-decoding/problem)

```cpp
void decode_huff(node * root,string s)
{
    node* temp = root;
    for (char c : s) {
        if(c=='0'){
            temp = temp->left;
        }else{
            temp = temp->right;
        }
        if (temp->left==NULL && temp->right==NULL) {
            cout << temp->data;
            temp = root;
        }
    }
}
```

[Binary Search Tree : Lowest Common Ancestor](https://www.hackerrank.com/challenges/binary-search-tree-lowest-common-ancestor/problem)

```cpp
Node *lca(Node *root, int v1,int v2) {
    // Write your code here.
    if(root->data < v1 && root->data < v2){
        return lca(root->right,v1,v2);
    }
    
    if(root->data > v1 && root->data > v2){
        return lca(root->left,v1,v2);
    }

    return root;   
}
```

[Swap Nodes [Algo]](https://www.hackerrank.com/challenges/swap-nodes-algo/problem)

```cpp
#include <algorithm>
#include <cmath>
#include <cstdio>
#include <vector>
#include <iostream>
#include <algorithm>
using namespace std;
 
#define MAXN 1024
 
 
int l[MAXN + 1], r[MAXN + 1], d[MAXN + 1], n, t, k;

void calc_depth(int cur, int depth)
{
    d[cur] = depth;
    if (l[cur] > 0) calc_depth(l[cur], depth + 1);
    if (r[cur] > 0) calc_depth(r[cur], depth + 1);
}
 
void in_order(int cur)
{
    if (l[cur] > 0) in_order(l[cur]);
    cout << cur << " ";
    if (r[cur] > 0) in_order(r[cur]);
}
 
int main()
{
    cin >> n;
    for (int i = 1; i <= n; i++) {
        cin >> l[i] >> r[i];
    }
 
    calc_depth(1, 1);
 
    cin >> t;
    while (t--) {
        cin >> k;
 
        for (int i = 1; i <= n; i++) {
            if (d[i] % k == 0) {
                swap(l[i], r[i]);
            }
        }

        in_order(1);
        cout << endl;
    }
    return 0;
}
```