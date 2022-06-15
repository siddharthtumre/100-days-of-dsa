---
title: "Day 56 - Hacker Data Structures(Trees)"
date: "2022-06-14"
---

[Tree: Preorder Traversal](https://www.hackerrank.com/challenges/tree-preorder-traversal/problem)

```cpp
void preOrder(Node *root) {
    if(root==NULL){
        return;
    }
    cout<<root->data<<" ";
    preOrder(root->left);
    preOrder(root->right);
}
```

[Tree: Postorder Traversal](https://www.hackerrank.com/challenges/tree-postorder-traversal/problem)

```cpp
void postOrder(Node *root) {
    if(root==NULL){
        return;
    }
    postOrder(root->left);
    postOrder(root->right);
    cout<<root->data<<" ";
}
```

[Tree: Inorder Traversal](https://www.hackerrank.com/challenges/tree-inorder-traversal/problem)

```cpp
void inOrder(Node *root) {
    if(root==NULL){
    return;
    }
    inOrder(root->left);
    cout<<root->data<<" ";
    inOrder(root->right);
}
```

[Tree: Height of a Binary Tree](https://www.hackerrank.com/challenges/tree-height-of-a-binary-tree/problem)

```cpp
int height(Node* root) {
    // Write your code here.
    if(root==NULL){
        return -1;
    }
    int left, right;
    left=height(root->left);
    right=height(root->right);
    
    return max(left,right) + 1;
}
```

[Tree : Top View](https://www.hackerrank.com/challenges/tree-top-view/problem)

```cpp
void calculateDistance(Node *root, int h, int l, map<int,pair<int, int>> &d){
    if(root==NULL){
        return;
    }
    
    if(d.count(h) == 0){
        d[h] = make_pair(root->data, l);
    }else if (d[h].second > l) {
        d[h] = make_pair(root->data, l);
    }
    calculateDistance(root->left, h-1, l+1, d);
    calculateDistance(root->right, h+1, l+1, d);
}

void topView(Node * root) {
    map<int,pair<int, int>> d;
    calculateDistance(root, 0, 0, d);
    
    map<int,pair<int, int>>::iterator it;
    
    for(it=d.begin(); it!=d.end(); it++){
        cout<<it->second.first<<" ";
    }
}
```

[Tree: Level Order Traversal](https://www.hackerrank.com/challenges/tree-level-order-traversal/problem)

```cpp
void levelOrder(Node * root) {
    queue<Node*> q;
    q.push(root);
    
    while(q.empty() == false){
        Node *node = q.front();
        cout<<node->data<<" ";
        q.pop();
        
        if(node->left!=NULL){
            q.push(node->left);
        }
        if(node->right!=NULL){
            q.push(node->right);
        }
    }
}
```

