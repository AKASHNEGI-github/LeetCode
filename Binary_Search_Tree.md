# Binary Search Tree

---
| Easy | Medium | Hard |
| ---- | ------ | ---- |
| ---- | ------ | Maximum Sum BST in Binary Tree |
---

- Maximum Sum BST in Binary Tree
```c++
class Prop{
public:
    int sum;
    int mini;
    int maxi;
    bool isBST;

    Prop() {
        sum = 0;
        mini = INT_MAX;
        maxi = INT_MIN;
        isBST = true;
    }
};

class Solution {
public:
    Prop* postOrderTraversal(TreeNode* root , int &maxSum)
    {
        if(root == NULL)
        {
            Prop* p = new Prop();
            return p;
        }
        Prop* leftSubTree = postOrderTraversal(root->left , maxSum);
        Prop* rightSubTree = postOrderTraversal(root->right , maxSum);

        Prop* current = new Prop();
        current->mini = min(root->val , leftSubTree->mini);
        current->maxi = max(root->val , rightSubTree->maxi);
        current->sum = root->val + leftSubTree->sum + rightSubTree->sum;
        current->isBST = (leftSubTree->isBST == true && rightSubTree->isBST == true) && (leftSubTree->maxi < root->val && root->val < rightSubTree->mini);
        if(current->isBST)
        {
            maxSum = max(current->sum , maxSum);
        }
        return current;
    }

    int maxSumBST(TreeNode* root) 
    {
        int maxSum = 0;
        Prop* p = postOrderTraversal(root , maxSum);
        return maxSum;
    }
};
```

---
