---
title: "Day 10 - Binary Trees & Binary Search Trees"
date: "2022-06-18"
---

[Valid BST From Preorder](https://www.interviewbit.com/problems/valid-bst-from-preorder/)

```cpp
bool canRepresentBST(vector<int>& pre, int n) 
{
    stack<int> s; 
  
    int root = INT_MIN; 
  
    for (int i=0; i<n; i++) 
    { 
        if (pre[i] < root) 
            return false; 
  
        while (!s.empty() && s.top()<pre[i]) 
        { 
            root = s.top(); 
            s.pop(); 
        } 
        s.push(pre[i]); 
    } 
    return true; 
} 

int Solution::solve(vector<int> &A) {
    set<int>s;
    for(int a:A){
        s.insert(a);
    }
    if(s.size() != A.size()){
        return 0;
    }
    if(canRepresentBST(A,A.size()))
        return 1;
    return 0; 
}
```

[Recover Binary Search Tree](https://www.interviewbit.com/problems/recover-binary-search-tree/)

```cpp
 void inorder(TreeNode *root, vector<int> &arr){
     if(root==NULL){
         return;
     }
     inorder(root->left, arr);
     arr.push_back(root->val);
     inorder(root->right, arr);
 }
 
vector<int> Solution::recoverTree(TreeNode* A) {
    vector<int> temp;
    inorder(A, temp);
    
    vector<int> ans;
    
    int first=0, second=0;
    int count=0;
    for (int i = 1; i < temp.size(); i++) {
        if (temp[i] < temp[i - 1]) {
            count++;
            if (first == 0)
                first = i;
            else
                second = i;
        }
    }
    if (count == 2){
        ans.push_back(temp[second]);
        ans.push_back(temp[first-1]);
    }
    else if (count == 1){
        ans.push_back(temp[first]);
        ans.push_back(temp[first - 1]);
    }
    
    return ans;
}
```