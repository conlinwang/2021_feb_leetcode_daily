# 538 Convert BST to Greater Tree

Given the `root` of a Binary Search Tree (BST), convert it to a Greater Tree such that every key of the original BST is changed to the original key plus sum of all keys greater than the original key in BST.

As a reminder, a *binary search tree* is a tree that satisfies these constraints:

- The left subtree of a node contains only nodes with keys **less than** the node's key.
- The right subtree of a node contains only nodes with keys **greater than** the node's key.
- Both the left and right subtrees must also be binary search trees.

**Note:** This question is the same as 1038: [https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree/](https://leetcode.com/problems/binary-search-tree-to-greater-sum-tree/)

**Example 1:**

![https://assets.leetcode.com/uploads/2019/05/02/tree.png](https://assets.leetcode.com/uploads/2019/05/02/tree.png)

```
Input: root = [4,1,6,0,2,5,7,null,null,null,3,null,null,null,8]
Output: [30,36,21,36,35,26,15,null,null,null,33,null,null,null,8]

```

**Example 2:**

```
Input: root = [0,null,1]
Output: [1,null,1]

```

**Example 3:**

```
Input: root = [1,0,2]
Output: [3,3,2]

```

**Example 4:**

```
Input: root = [3,2,4,1]
Output: [7,9,4,10]

```

**Constraints:**

- The number of nodes in the tree is in the range `[0, 104]`.
- `104 <= Node.val <= 104`
- All the values in the tree are **unique**.
- `root` is guaranteed to be a valid binary search tree.

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def convertBST(self, root: TreeNode) -> TreeNode:
        if not root:
            return root
        self.res = 0
        def dfs(node):
            if not node:
                return
            if node.right:
                dfs(node.right)
            node.val += self.res
            self.res = node.val
            if node.left:
                dfs(node.left)
        dfs(root)
        return root
```

T.C. O(N), S.C. O(N)

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
private:
    int cur = 0;
public:
    void dfs(TreeNode* node) {
        if (!node)
            return;
        if (node->right)
            dfs(node->right);
        cur += node->val;
        node->val = cur;
        if (node->left)
            dfs(node->left);
    }
    TreeNode* convertBST(TreeNode* root) {
        dfs(root);
        return root;        
    }
};
```