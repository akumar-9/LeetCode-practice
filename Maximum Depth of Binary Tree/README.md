# Maximum Depth of Binary Tree

# Problem Statement
Given the `root` of a binary tree, return its maximum depth.

A binary tree's maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.
### Example
Input: root = [3,9,20,null,null,15,7] Output: 3
## Approach
I use DFS to recursively find the depth of the left subtree and right subtree and the greater of them. 
### Time Complexity
- **O(n)**:where `n` is the number of the nodes in the tree.
### Space Complexity
- **O(h)**:The recursive call stack uses space proportional to the height of the tree(h).
## Solution Code
```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
public class Solution {
    public int MaxDepth(TreeNode root) {
        if(root == null){
            return 0;
        }
        return 1 + Math.Max(MaxDepth(root.left), MaxDepth(root.right));
    }
}