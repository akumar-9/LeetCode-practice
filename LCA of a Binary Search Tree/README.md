# LCA of a Binary Search Tree

# Problem Statement
Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow a node to be a descendant of itself).”
### Example
Input: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
Output: 6
Explanation: The LCA of nodes 2 and 8 is 6.

## Approach
I check if the nodes p and q are on the same side by comparing their values with root. If both p and q are less than the root, search for LCA in left subtree, if both are greater than root, search in right subtree. I the nodes lie on the either side then it means I have reached the LCA and if I go deeper in any direction then I have no common ancestor.
### Time Complexity
- **O(N)**:Each node in the tree is visited in the worst case.
### Space Complexity
- **O(H)**: Depth of recursion stack 
## Solution Code
```C#
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left;
 *     public TreeNode right;
 *     public TreeNode(int x) { val = x; }
 * }
 */

public class Solution {
    public TreeNode LowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        TreeNode curr = root;

        while(curr!=null){
            if(p.val < curr.val && q.val < curr.val)
                curr = curr.left;
            else if(p.val > curr.val && q.val > curr.val)
                curr = curr.right;
            else
            return curr;
        }
        return null;
    }
}