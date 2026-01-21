# Binary Tree

---
| Easy | Medium | Hard |
| ---- | ------ | ---- |
| Binary Tree Inorder Traversal | ------ | ---- |
| Binary Tree Preorder Traversal | ------ | ---- |
| Binary Tree Postorder Traversal | ------ | ---- |
| Maximum Depth of Binary Tree | ------ | ---- |
| Minimum Depth of Binary Tree | ------ | ---- |
---

### Easy

- Binary Tree Inorder Traversal
```c++

```

```c++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) // Morris InOrder Traversal
    {
        vector<int> ans;
        TreeNode* current = root;
        while(current != NULL)
        {
            if(current->left == NULL)
            {
                ans.push_back(current->val);
                current = current->right;
            }
            else
            {
                TreeNode* previous = current->left;
                while(previous->right != NULL && previous->right != current)
                {
                    previous = previous->right;
                }
                if(previous->right == NULL)
                {
                    previous->right = current;
                    current = current->left;
                }
                else
                {
                    previous->right = NULL;
                    ans.push_back(current->val);
                    current = current->right;
                }
            }
        }
        return ans;
    }
};
```

- Binary Tree Preorder Traversal
```c++

```

```c++
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) // Morris PreOrder Traversal
    {
        vector<int> ans;
        TreeNode* current = root;
        while(current != NULL)
        {
            if(current->left == NULL)
            {
                ans.push_back(current->val);
                current = current->right;
            }
            else
            {
                TreeNode* previous = current->left;
                while(previous->right != NULL && previous->right != current)
                {
                    previous = previous->right;
                }
                if(previous->right == NULL)
                {
                    ans.push_back(current->val);
                    previous->right = current;
                    current = current->left;
                }
                else
                {
                    previous->right = NULL;
                    current = current->right;
                }
            }
        }
        return ans;   
    }
};
```

- Binary Tree Postorder Traversal
```c++

```

```c++
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) // Morris PostOrder Traversal
    {
        vector<int> ans;
        TreeNode* current = root;
        while(current != NULL)
        {
            if(current->right == NULL)
            {
                ans.push_back(current->val);
                current = current->left;
            }
            else
            {
                TreeNode* previous = current->right;
                while(previous->left != NULL && previous->left != current)
                {
                    previous = previous->left;
                }
                if(previous->left == NULL)
                {
                    ans.push_back(current->val);
                    previous->left = current;
                    current = current->right;
                }
                else
                {
                    previous->left = NULL;
                    current = current->left;
                }
            }
        }
        reverse(ans.begin() , ans.end());
        return ans;   
    }
};
```

- Maximum Depth of Binary Tree
```c++
class Solution {
public:
    int maxDepth(TreeNode* root) 
    {
        if(root == NULL)
        {
            return 0;
        }   
        int heightLeftSubTree = maxDepth(root->left);
        int heightRightSubTree = maxDepth(root->right);
        return max(heightLeftSubTree , heightRightSubTree) + 1;
    }
};
```

- Minimum Depth of Binary Tree
```c++
class Solution {
public:
    int minDepth(TreeNode* root) 
    {
        if(root == NULL)
        {
            return 0;
        }
        int heightLeftSubTree = minDepth(root->left);
        int heightRightSubTree = minDepth(root->right);
        if(heightLeftSubTree == 0 || heightRightSubTree == 0)
        {
            return max(heightLeftSubTree , heightRightSubTree) + 1;
        }
        return min(heightLeftSubTree , heightRightSubTree) + 1;
    }
};
```
