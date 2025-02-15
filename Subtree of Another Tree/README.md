# Subtree of Another Tree

# Problem Statement
Given the roots of two binary trees `root` and `subRoot`, return `true` if there is a subtree of `root` with the same structure and node values of `subRoot` and `false` otherwise.

A subtree of a binary tree tree is a tree that consists of a node in tree and all of this node's descendants. The tree tree could also be considered as a subtree of itself.
### Example
Input: root = [3,4,5,1,2], subRoot = [4,1,2]
Output: true

## Approach
I use recursion and tree matching. Find a node that matches the subRoot. Check if the trees are identical(sameTree) starting from that node. 
### Time Complexity
- **O(R*S)**:Each node in `root` is visited once (R). Each node in `subRoot` is compared (S).
### Space Complexity
- **O(R+ S)**:This occurs when root is a skewed tree, meaning recursion could go as deep as O(N). Additionally, in the worst case, IsSameTree() is called for a tree of size S, adding an extra O(S).
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
    public bool IsSubtree(TreeNode root, TreeNode subRoot) {

        if(root == null){
            return false;
        }

        if(subRoot == null){
            return true;
        }

        if(IsSameTree(root, subRoot)){
            return true;
        }

        return IsSubtree(root.left, subRoot) || IsSubtree(root.right, subRoot);
    }

        private bool IsSameTree(TreeNode p, TreeNode q){
            if(p == null && q == null){
                return true;
            }
            if(p == null || q == null){
                return false;
            }
            if(p.val != q.val){
                return false;
            }
            return IsSameTree(p.left, q.left) && IsSameTree(p.right, q.right);

        }
    
}