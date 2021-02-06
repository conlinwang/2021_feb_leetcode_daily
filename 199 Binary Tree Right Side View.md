# 199 Binary Tree Right Side View

Given a binary tree, imagine yourself standing on the *right* side of it, return the values of the nodes you can see ordered from top to bottom.

**Example:**

```
Input: [1,2,3,null,5,null,4]
Output: [1, 3, 4]
Explanation:

   1            <---
 /   \
2     3         <---
 \     \
  5     4       <---

```

python solution:

```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def rightSideView(self, root: TreeNode) -> List[int]:
        res = []
        if not root:
            return res
        q = [root]
        while q:
            right_sight = []
            level_q = q[:]
            q = []
            for node in level_q:
                right_sight = [node.val]
                if node.left:
                    q.append(node.left)
                if node.right:
                    q.append(node.right)
            res.append(right_sight[0])
        return res
```

T.C. → O(N)

S.C. → O(N)