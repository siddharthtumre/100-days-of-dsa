---
title: "Day 8 - Binary Trees & Binary Search Trees"
date: "2022-06-16"
---

[Binary Tree Morris Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/)

```cpp
vector<int> inorderTraversal(TreeNode* root) {
    vector<int>ans;
    TreeNode *cur = root;
    while (cur != NULL) {
        if (cur -> left == NULL) {
            ans.push_back(cur->val);
            cur = cur -> right;
        } else {
            TreeNode *prev = cur->left;
            while (prev->right != NULL && prev->right!=cur) {
            prev = prev -> right;
            }

            if (prev -> right == NULL) {
            prev->right=cur;
            cur=cur->left;
            } else {
            prev->right = NULL;
            ans.push_back(cur->val);
            cur = cur->right;
            }
        }
        }
    return ans;
}
```

[Binary Tree Morris Inorder Traversal](https://leetcode.com/problems/binary-tree-preorder-traversal/)

```cpp
vector<int> preorderTraversal(TreeNode* root) {
    vector<int>ans;
    TreeNode *cur = root;
    while (cur != NULL) {
        if (cur -> left == NULL) {
            ans.push_back(cur->val);
            cur = cur -> right;
        } else {
            TreeNode *prev = cur->left;
            while (prev->right != NULL && prev->right!=cur) {
	            prev = prev -> right;
            }

            if (prev -> right == NULL) { // Only one change in when we add an element to the answer array
	            prev->right=cur;
	            ans.push_back(cur->val); 
	            cur=cur->left;
	            } else {
	            prev->right = NULL;
	            cur = cur->right;
            }
        }
    }
    return ans;
}
```

## Binary Search Trees - Insertion

```cpp
class Node{
public:
    int data;
    Node* left;
    Node* right;

    Node(int value){
        data = value;
        left = right = NULL;
    }
};
class BST{
public:
    Node *root;
    BST(){
        root = NULL;
    }

    void insert(Node* node){
        if(root==NULL){
            root=node;
        }else{
            Node *temp = root;
            while(temp!=NULL){
                if(node->data == temp->data){
                    return;
                }else if(node->data > temp->data && temp->right == NULL){
                    temp->right = node;
                    break;
                }else if (node->data > temp->data){
                    temp = temp->right;
                }else if(node->data < temp->data && temp->left == NULL){
                    temp->left = node;
                    break;
                }else {
                    temp = temp->left;
                }
                
            }
        }
    }
};
```

[left View of Binary Search Tree](https://www.hackerrank.com/contests/smart-interviews/challenges/si-left-view-of-tree)
```cpp
void leftView(Node *root, size_t level, vector<int> &ans){
    if(root==NULL){
        return;
    }
    if(ans.size()==level)
        ans.push_back(root->data);
    leftView(root->left, level+1, ans);
    leftView(root->right, level+1, ans);
}
```

[Right View of Binary Search Tree](https://leetcode.com/problems/binary-tree-right-side-view/)

```cpp
void rightView(Node *root, size_t level, vector<int> &ans){
    if(root==NULL){
        return;
    }
    if(ans.size()==level)
        ans.push_back(root->data);
    rightView(root->right, level+1, ans);
    rightView(root->left, level+1, ans);
}
```
