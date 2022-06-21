---
title: "Day 9 - Binary Trees & Binary Search Trees"
date: "2022-06-17"
---

[Is Balanced Tree](https://www.hackerrank.com/contests/smart-interviews/challenges/si-is-balanced-tree)
```cpp
int height(Node* node)
{
    if (node == NULL)
        return 0;
    
    return 1 + max(height(node->left),
                   height(node->right));
}

bool isBalanced(Node *root){
    int left, right;
    
    if (root == NULL)
        return 1;
 
    left = height(root->left);
    right = height(root->right);
 
    if (abs(left - right) <= 1 && isBalanced(root->left) && isBalanced(root->right))
        return 1;
 
    return 0;
}
```

[Populating Next Right Pointers in Each Node](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)
```cpp
class Solution {
public:
    Node* connect(Node* root) {
        if(root==NULL){
            return root;
        }
        queue<Node *>q;
        q.push(root);
        while(!q.empty()){
            int siz = q.size();
            while(siz--){
                Node *temp = q.front();
                q.pop();
                if(siz>0){
                    temp->next = q.front();
                }else{
                    temp->next = NULL;
                }
                
                if(temp->left!=NULL){
                    q.push(temp->left);
                }
                if(temp->right!=NULL){
                    q.push(temp->right);
                }
            }
        }
        return root;
    }
};
```

[Is Complete Binary Tree](https://www.hackerrank.com/contests/smart-interviews/challenges/si-is-complete-binary-tree/submissions/code/1345890865)

```cpp
bool isCompleteBinaryTree(Node *root){
    queue<Node *>q;
    q.push(root);
    
    bool flag = false;
    while(!q.empty()){
        Node *temp = q.front();
        q.pop();
        if(temp==NULL){
            flag = true;
        }else{
            if(flag){
                return false;
            }
            q.push(temp->left);
            q.push(temp->right);
        }
    }
    return true;
}
```