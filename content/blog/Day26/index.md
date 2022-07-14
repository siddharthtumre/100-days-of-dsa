---
title: "Day 26 - Binary Tree"
date: "2022-07-04"
---

[Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

```cpp
class Solution {
public:
    TreeNode* solve(vector<int>& inorder, vector<int>& preorder, int start, int end, int& idx) {
        if (start > end) return NULL;
        int pivot = start;
        while(inorder[pivot] != preorder[idx]) pivot++;
        
        idx++;
        TreeNode* newNode = new TreeNode(inorder[pivot]);
        newNode->left = solve(inorder, preorder, start, pivot-1, idx);
        newNode->right = solve(inorder, preorder, pivot+1, end, idx);
        return newNode;
    }
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
		int n = inorder.size();
        int idx = 0;
        return solve(inorder, preorder, 0, n-1, idx);
    }
};
```

[Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

```cpp
class Solution {
public:
    TreeNode* solve(vector<int>& in, vector<int>& pos, int start, int end, int& idx){
        if(start>end){
            return NULL;
        }
        
        int pivot = start;
        while(in[pivot] != pos[idx]) pivot++;
        
        idx--;
        TreeNode* newNode = new TreeNode(in[pivot]);
        newNode->right = solve(in, pos, pivot+1, end, idx);
        newNode->left = solve(in, pos, start, pivot-1, idx);
        return newNode;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        int n = inorder.size();
        int idx = n-1;
        return solve(inorder, postorder, 0, n-1, idx);
        
    }
};
```