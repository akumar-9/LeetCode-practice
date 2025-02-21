# Kth Smallest Element in a BST

# Problem Statement
Given the root of a binary search tree, and an integer k, return the kth smallest value (1-indexed) of all the values of the nodes in the tree.
### Example
Input: root = [3,1,4,null,2], k = 1
Output: 1

## Approach
Take advantage of binary search tree's sorted inorder traversal. I traverse the BST inorder and keep count of the visited nodes. Once k elements are visited, return the curren node. (Basically, if a sorted list is given, we would return the kth element from the start)
### Time Complexity
- **O(N)**:Full traversal O(N) when k = N.
### Space Complexity
- **O(H)**: Recursive call stack depth.
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
    int result = 0;
    int count = 0;
    public int KthSmallest(TreeNode root, int k) {
        Inorder(root, k);
        return result;
    }

    private void Inorder(TreeNode root, int k){
        if(root == null)    return;

        Inorder(root.left, k);
        
        count++;
        if(count == k){
            result = root.val;
            return;
        }
        
        Inorder(root.right,k);
    }
}