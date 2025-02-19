# Validate Binary Search Tree

# Problem Statement
Given the `root` of a binary tree, determine if it is a valid binary search tree (BST).

A valid BST is defined as follows:

1. The left subtree of a node contains only nodes with keys less than the node's key.
2. The right subtree of a node contains only nodes with keys greater than the node's key.
3. Both the left and right subtrees must also be binary search trees.
### Example
Input: root = [2,1,3]
Output: true
## Approach
I use the min/max bound approach. Each node's value in the BST is bounded by the root. The left subtree is always smaller than parent. Right subtree is always greater than parent. 
### Time Complexity
- **O(N)**:Each node in the tree is visited.
### Space Complexity
- **O(H)**: Recursive stack depth. Worst case is O(n) for skewed tree, O(logn) for balanced tree.
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
    public bool IsValidBST(TreeNode root) {

        return IsValid(root, long.MinValue, long.MaxValue);

        bool IsValid(TreeNode root, long min, long max){
            if(root == null){
                return true;
            }
            if( root.val <= min || root.val >= max){
                return false;
            }
            return IsValid(root.left, min, root.val) && IsValid(root.right, root.val, max);
        }
    }
}