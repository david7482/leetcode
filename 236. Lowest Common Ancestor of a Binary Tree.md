# 236. Lowest Common Ancestor of a Binary Tree (Medium)

## Problem
Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we allow a node to be a descendant of itself).”

Given the following binary tree:  root = [3,5,1,6,2,0,8,null,null,7,4]

```
        _______3______
       /              \
    ___5__          ___1__
   /      \        /      \
   6      _2       0       8
         /  \
         7   4
```

**Example 1:**

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of of nodes 5 and 1 is 3.
```

**Example 2:**
```
Input: root = [1,2], p = 1, q = 2
Output: 1
```

## Solution

### Recursion

For a given root, recursively call LCA(root.left, p, q) and LCA(root.right, p, q).  
If both returns a valid node which means p, q are in different subtrees, then root will be their LCA.  
If only one valid node returns, which means p, q are in the same subtree, return that valid node as their LCA.

* Time: O(n)
* Space: O(h)

```cpp
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == nullptr) {
            return nullptr;
        }
        
        if (root->val == p->val || root->val == q->val) {
            return root;
        }
        
        auto left = lowestCommonAncestor(root->left, p, q);
        auto right = lowestCommonAncestor(root->right, p, q);
        if (left != nullptr && right != nullptr) {
            return root;
        }
        if (left != nullptr) {
            return left;
        }
        if (right != nullptr) {
            return right;
        }
        
        return nullptr;
    }
};
```