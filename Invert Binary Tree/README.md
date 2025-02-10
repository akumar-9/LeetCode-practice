# Invert Binary Tree

# Problem Statement
Given the `root` of a binary tree, invert the tree, and return its root.

### Example
Input: root = [4,2,7,1,3,6,9] Output: [4,7,2,9,6,3,1]
## Approach
Inverting is just swapping the left and right subtree. I recursively invert the left subtree and then the right subtree and then swap them.
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
    public TreeNode InvertTree(TreeNode root) {
        if(root == null){
            return null;
        }

        TreeNode tmp = root.left;
        root.left = InvertTree(root.right);
        root.right = InvertTree(tmp);
        return root;
    }
}