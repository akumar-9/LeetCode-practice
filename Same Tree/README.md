# Same Tree

# Problem Statement
Given the roots of two binary trees `p` and `q`, write a function to check if they are the same or not.

Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.
### Example
Input: p = [1,2,3], q = [1,2,3] Output: true
## Approach
I check if the given two nodes are equal, then I check if the left subtree of both nodes are equal, then check if the right subtree of both nodes are equal. 
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
    public bool IsSameTree(TreeNode p, TreeNode q) {
        if(p == null && q == null){
            return true;
        }
        if(p == null || q == null){
            return false;
        }
        if(p.val != q.val){
            return false;
        }
        return IsSameTree(p.left, q.left) && IsSameTree(p.right,q.right);
    }
}